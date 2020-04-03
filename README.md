# pean-strava
Test repo to play around with PEAN stack and STRAVA API.

Originally based on "Create a MEAN app with Angular and Docker Compose" from https://scotch.io/tutorials/create-a-mean-app-with-angular-2-and-docker-compose

**Building**
* Open command window in the root folder ($).
* $ docker-compose build (builds the app -- only needed if changes were made since last build)
* $ docker-compose up (runs the app -- wait until the message ```** Angular Live Development Server is listening on 0.0.0.0:4200, open your browser on http://localhost:4200/ **```
appears in the console output)
* Open browser at http://localhost:4200
* Also try http://localhost:4200/users (the app re-inits the database each time it runs. Try adding, finding, removing users)

GitHub authentication notes:
For now the app just makes the auth call to GitHub but doesn't do anything with the results. You can test by
logging out of GitHub on their page and then clicking the GitHub button on this app's page. You should be redirected to
the GitHub login page. After you login to GitHub successfully, you should be redirected to this app's login page. 

Authentication flow -
* Register app (ApplicationName, HomepageURL, ApplicationCallbackURL) for authentication at GitHub: https://github.com/settings/applications/new
* Get ClientID and ClientSecret from: https://github.com/settings/developers
* NodeJS/Express app process flow:
  * From the browser, client makes a request to https://github.com/login/oauth/authorize GitHub endpoint with ClientID
  * GitHub endpoint authorizes client using the Github login and redirects to the ApplicationCallbackURL with a new RequestToken
  * Client uses RequestToken, ClientID and ClientSecret to ask GitHub API for an AccessToken
  * If all the provided values are valid, GitHub API will respond with an AccessToken for client to make authorised requests
