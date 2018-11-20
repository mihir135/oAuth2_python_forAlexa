# oAuth2_python_forAlexa
An oAuth2.0 server in python. This demo is used for Alexa Skill's account link.

```
url = [
    (r'/oa2/auth', Oa2AuthHandle),
    (r'/oa2/token', Oa2TokenHandle),
    (r'/oa2/login', Oa2LoginHandle),
]
```
Where /oa2/auth is the Authorization URL in Account Linking in the skill configuration.
/oa2/login is the URL submitted by the login button in login.html.
/oa2/token is the interface that alexa periodically obtains tokens from the oauth2 server.

The specific process is:
1. When the user activates the skill you developed on the alexa app, it will call the /oa2/auth interface and go to the login.html page (the login page of your system);
2, the user uses your system's account and password to log in, click connect, call /oa2/login;
3. User password verification in /oa2/login, return to the redirect page after successful (alexa prompt page), and return a code (you customize, associate with user);
4, alexa call /oa2/token to get the token regularly, you need to check the code and client_id, and then return tocken and refreshtoken. This token will be the scope/token of each request in the skill. This will determine which user received the message each time your skill received.
5. After the enable skill is finished, there will be a discovery action. You only need to process the discover command in the skill and return the list of devices under the corresponding token (user).
