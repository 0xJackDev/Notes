

JWT also known as Json Web Tokens.


JavaScript Object Signing and Encryption (JOSE) is a framework specifying ways to securely transmit information on the internet. Its most well known for JWT's. JWTs are used for auth and they do this by storing your "login session" in your browser after you have authenticated yourself by entering your username and password. In other words, the web-site gives you a JWT that contains your user ID and can be presented to the site to prove who you are.


You can recognize JWTs because its base64 encoded data split into three parts seperated by a period (.) This includes the header, the payload, and the signature. In fact its a variant of base64 encoding where the + and / have been replaced by different special characters since they can cause issues in URLs.


Some developers belive JWT is like encryption and put sensitive data inside a token. However you can decode this easily with the PyJWT library


https://pyjwt.readthedocs.io/en/stable/


For the first challenge we must simply decode the JWT While normally i would use

https://jwt.is/ I will use the python library.

However the decode function usually requires you to verify that is correct. But we can decode it and view the JSON as it is just base64 encoded. So we can use 

## Reading the Claimset without Validation[](https://pyjwt.readthedocs.io/en/2.8.0/usage.html#reading-the-claimset-without-validation "Permalink to this headline")

If you wish to read the claimset of a JWT without performing validation of the signature or any of the registered claim names, you can set the `verify_signature` option to `False`.

Note: It is generally ill-advised to use this functionality unless you clearly understand what you are doing. Without digital signature information, the integrity or authenticity of the claimset cannot be trusted.

>>> jwt.decode(encoded, options={"verify_signature": False})
{'some': 'payload'}





## JWT Sessions


The traditional way to store sessions is with session ID cookies. After you login to a website, a session object is created for you on the backend server and your browser is given a cookie which identifies that object. As you make requests to a site your browser automatically sends the session ID cookie to the backend server, which uses that ID to find your session in its own memory and thus by having that "session-id"/cookie you can authorize you to perform different actions


JWTs work differently. After you login, the server sends your web browser the whole session object in a JWT, containing a payload of key-value pairs describing your username, privileges, and other info. Also included is signature created using the servers secret key. Your web browser saves the saves the token into local storage.

  
![diagram showing JWT usage](https://cryptohack.org/static/img/jwt-usage.png)


On subsequent requests, your browser sends the token to the backend server. The server verifies the signature first, and then reads the token payload to authorize you.  
  
To summaries, with session ID cookies, sessions live on the server, but with JWTs, sessions live on the client.


The main advantage to JWTs over session ID cookies is that they are easy to scale. Organisations need a way to share sessions across multiple backend servers. When a client switches from using one server to another (which happens alot when using CDNs like cloud flare) when using JWT the clients session should still work.


There are some downsides to JWTs as they are often configured in a insecure way and clients are free to modify them and see if the server will verify them. We will look at these exploits in the next challenges. 

They send JWT's over a Authorization Header




## JWT secrets

The most common signing algorithms used in JWTs are HS256 and RS256. The first is a symmetric signing scheme using HMAC (Hash-based Message Authentication Code) with a SHA256 hash function.  RS256 is a asymmetric signing scheme. 


Alot of guides say to use HS256 as its easier. The secret key is used to sign a token and the same key is used to verify it.

However if the signing secret key is compromised an attacker cam call arbitrary tokens and forge sessions of other users, potentially causing total compromise of a webapp.  HS256 makes the secret key harder to secure then a asymmetric keypair as the key that crafts token  must be available on all servers that verify HS256 tokens (unless better infrastructure with a seperate token verifying service is in place which usually isnt the case). In contrast with RS256 the signing key can be better protected while the verifying key can be distrubuted freely.


Here is a snipped of source code in which I have to create a JWT session with admin permission



```
import jwt # note this is the PyJWT module, not python-jwt


SECRET_KEY = ? # TODO: PyJWT readme key, change later
FLAG = ?


@chal.route('/jwt-secrets/authorise/<token>/')
def authorise(token):
    try:
        decoded = jwt.decode(token, SECRET_KEY, algorithms=['HS256'])
    except Exception as e:
        return {"error": str(e)}

    if "admin" in decoded and decoded["admin"]:
        return {"response": f"Welcome admin, here is your flag: {FLAG}"}
    elif "username" in decoded:
        return {"response": f"Welcome {decoded['username']}"}
    else:
        return {"error": "There is something wrong with your session, goodbye"}


@chal.route('/jwt-secrets/create_session/<username>/')
def create_session(username):
    encoded = jwt.encode({'username': username, 'admin': False}, SECRET_KEY, algorithm='HS256')
    return {"session": encoded}

```

Notice how the secret key is set to the PyJWT key which is "secret" well now since we know that we can just make our own jwt encoding scheme which encodes the json 'username': 'admin', 'admin': True. Like this


https://pyjwt.readthedocs.io/en/2.8.0/usage.html


As seen in the examples is whre i got ther key





## RSA or HMAC

Theres another issue caused by allowing attackers to specify their own algorithms but not carefully validating. Attackers can mix and match the algorithms that are used to sign and verify data. When one of these is a symmetric algorithm and one is an asymmetric algorithm this creates a beautifal vuln . 

The server is running PyJWT with a small patch to enable an exploit that existed in PyJWT versions <= 1.5.0. To create the malicious signature, you will need to patch your PyJWT library too. If you want to patch, look at the line that was added in the [fix for the vulnerability](https://github.com/jpadilla/pyjwt/commit/37926ea0dd207db070b45473438853447e4c1392). Use `pip show pyjwt` to find the location of the PyJWT library on your computer, and make the edit. For versions of PyJWT > 2.4.0 the code has been changed so you will have to edit `jwt/utils.py` instead of `jwt/algorithms.py`
