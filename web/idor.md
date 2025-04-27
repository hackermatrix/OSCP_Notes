# IDOR

### Steps :thumbsup:

1. Create 2 accounts for the same web application.
2. Click each and every button on the website .
3. Go through all the requests to find requests containing user related variables.
4. Find out how this particular request is authenticating with the server.
   1. Auth Token (Authorization Headers) ?
   2. Cookie based Authentication ? (Then what variable is it using in the cookie ?)
5. Keep the data being sent the same and just replace the auth details for **User 1** to **User 2**
