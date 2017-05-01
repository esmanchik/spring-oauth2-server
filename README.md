# spring-oauth2-server
Minimal Spring Boot OAuth2 Server

good explanation of OAuth2 is here https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2

# build and launch
```
mvn package
java -jar target/oauth2-server-1.0.jar --server.port=8888 --server.contextPath=/v1
```

open in your browser

http://localhost:8888/v1/oauth/authorize/?response_type=code&client_id=fooClientIdPassword&redirect_uri=http://localhost:8888/v1/login&scope=read

enter admin as user name and nimda as a password - you should see auth code now (assume it is ap9F3I)

then do following to get access token
```
curl -u 'fooClientIdPassword:secret' http://localhost:8888/v1/oauth/token \
     -d 'client_id=fooClientIdPassword&client_secret=secret&grant_type=authorization_code&redirect_uri=http://localhost:8888/v1/login&code=ap9F3I'
```

you should get response similar to that one 

```
{"access_token":"6e6355fb-05ba-427d-97cd-7733950a5ba8","token_type":"bearer","refresh_token":"eafe9511-76a9-40c7-af3a-0047bab4dcb1","expires_in":3599,"scope":"read"}
```
