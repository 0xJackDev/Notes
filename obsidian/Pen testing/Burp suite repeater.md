In Burp suite you can use the render function to see the webpage normally as it would be in a web browser, Raw is the actual HTTP thing that's being sent and Pretty is Raw except de-obfuscated. and hex is that except the actually Hexadecimal response/request.

Inspector which is on the right side of both proxy and Repeater allows you to breakup the request into different smaller chunks like Headers/ cookies. Body, etc. For example in the request attributes we can change the Protocol from HTTP/2 to HTTP/1 or The other way around. 

1. **Request Query Parameters:** These refer to data sent to the server via the URL. For example, in a GET request like `https://admin.tryhackme.com/?redirect=false`, the query parameter **redirect** has a value of "false".
2. **Request Body Parameters:** Similar to query parameters, but specific to POST requests. Any data sent as part of a POST request will be displayed in this section, allowing us to modify the parameters before resending.
3. **Request Cookies:** This section contains a modifiable list of cookies sent with each request.
4. **Request Headers:** It enables us to view, access, and modify (including adding or removing) any headers sent with our requests. Editing these headers can be valuable when examining how a web server responds to unexpected headers.
5. **Response Headers:** This section displays the headers returned by the server in response to our request. It cannot be modified, as we have no control over the headers returned by the server. Note that this section becomes visible only after sending a request and receiving a response.


SELECT firstName, lastName, pfpLink, role, bio FROM people WHERE id = 2'

About | id,firstName,lastName,pfpLink,role,shortRole,bio,notes None

