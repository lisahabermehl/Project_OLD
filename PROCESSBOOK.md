# day 1
Thought about what project to do. Had 3 different ideas at the beginning of the day:
An app that uses the NS API: sends a notification when train is delayed or calculates if you have to walk or run if you want to catch a certain train based on minutes remaining and how fast you run / walk
An app that gives an overview of all the different models that people use for instruction based on feedback.
An app that uses the Google Calendar API: user is able to make a TODO list (what to do, how much time do you need to do this, when does this need to be done), using an algoritm the app integrates this TODO list in the existing Google Calendar of the user.

_IMPORTANT DECISIONS_
Chose to do the last one in the end. Because I think it’ll be the most handy. Wrote a [project proposal](https://github.com/lisahabermehl/Project/blob/master/README.md) for this.

# day 2
Started the day with a standup. Everyone explained what they were planning on doing. Gave each other some tips.

At first I was planning on letting the user log in with a FireBase account, and link this to their Google account to get access to their Google Calendar. But it might be possible to just use this Google account for both logging in and getting access to the calendar. So I’m going to look into this today, noting the possibilities down here.

After that I started working out my design document which is due tomorrow.

Came across this while researching Firebase and Google Calendar:
 The Firebase SDKs will automatically refresh Firebase ID tokens, but not Google access tokens. There is no way to currently do this with the current SDKs that I am aware of, unless you roll your own Google OAuth flow using custom authentication.
https://stackoverflow.com/questions/28932427/firebase-auth-and-google-calendar
At present Firebase only supports certain scopes. You can’t use the *calendar scopes to authenticate with Firebase auth.
Scopes are strings that enable access to particular resources, such as user data. You include a scope in certain authorization requests, which then displays appropriate permissions text in a consent dialog that is presented to a user. Once the user consents to the permissions, Google sends your app tokens, which identify the specific authorization grant. In other words, the scopes and tokens determine what user data the user gives your app permission to access.
The only real workaround here, to avoid authenticating separately against Google and Firebase, would be to manually authenticate against Google with the requested scopes, then pass that OAuth token into Firebase's authWithOAuthToken method. In other words, reverse the auth process to log in with Google and then re-use the token in Firebase.
Works when used like this
Auth.$authWithOAuthPopup('google', { remember: "default", scope: 'https://www.googleapis.com/auth/calendar', scope: 'email' }) .then(function (authData) {
Maar aan de andere kant bestaat dit ook:
https://zapier.com/zapbook/firebase/google-calendar/

En lijken mensen er een oplossing voor te hebben gevonden:
https://stackoverflow.com/questions/39914899/using-firebase-auth-to-access-the-google-calendar-api

Alleen inloggen met Google lijkt het handigst te zijn:
http://www.androidhive.info/2014/02/android-login-with-google-plus-account-1/

Maaaar voor Firebase gebruik je ook gewoon je google-account. Dus misschien kan het wel gewooon.

_IMPORTANT DECISIONS_
* Deze week richten op het ophalen van informatie van de Google Calendar.
* Richten op het weergeven van de calendar en het maken van de ToDo list, de rest komt later. 