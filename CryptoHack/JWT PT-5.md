
It is possible to abuse JWT public keys without a public key being public. This challenge takes RSA or HMAC one step farther. and now both a deeper knowledge of RSA maths and data formatting is involved. It's more realistic than the first part as web apps usually won't have a route disclosing their public key.

Honestly Im assuming this is just the first but i have to translate the public key from PEM format to OpenSSH format

```
import jwt
import requests

r = requests.get('https://web.cryptohack.org/rsa-or-hmac/get_pubkey/')
public_key_pem = r.json()["pubkey"].encode()

token = jwt.encode({'username': 'admin', 'admin': True}, public_key_pem, algorithm='HS256')

print(token)
```


https://www.vicarius.io/vsociety/posts/risky-algorithms-algorithm-confusion-in-pyjwt-cve-2022-29217


Now lets do this to translate.


Wait but How do i get the Public key?? hers the code

```
import jwt # note this is the PyJWT module, not python-jwt


# Private key generated using: openssl genrsa -out rsa-or-hmac-2-private.pem 2048
with open('challenge_files/rsa-or-hmac-2-private.pem', 'rb') as f:
   PRIVATE_KEY = f.read()
# Public key generated using: openssl rsa -RSAPublicKey_out -in rsa-or-hmac-2-private.pem -out rsa-or-hmac-2-public.pem
with open('challenge_files/rsa-or-hmac-2-public.pem', 'rb') as f:
   PUBLIC_KEY = f.read()

FLAG = ?


@chal.route('/rsa-or-hmac-2/authorise/<token>/')
def authorise(token):
    try:
        decoded = jwt.decode(token, PUBLIC_KEY, algorithms=['HS256', 'RS256'])
    except Exception as e:
        return {"error": str(e)}

    if "admin" in decoded and decoded["admin"]:
        return {"response": f"Welcome admin, here is your flag: {FLAG}"}
    elif "username" in decoded:
        return {"response": f"Welcome {decoded['username']}"}
    else:
        return {"error": "There is something wrong with your session, goodbye"}


@chal.route('/rsa-or-hmac-2/create_session/<username>/')
def create_session(username):
    encoded = jwt.encode({'username': username, 'admin': False}, PRIVATE_KEY, algorithm='RS256')
    return {"session": encoded}
```

We have to extract the RSA public key from a token that was signed with RS256



https://jwt.io/


great website


Lets use this

https://github.com/FlorianPicca/JWT-Key-Recovery


-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA7pgbuP6X8XHyFr47ybSr
1yT+m++FNn/fUnnKP113bYbcp/Jn4nl5kiRoK4cgXWv6yYaTxVMSyvLcdDkPsmZ0
J4DfBXZSpUKY2QK+oR76nb5fZ+VNUEi0Iu15GBJdIPj8yEA81OviDNcnXRyDpLBW
tXZ1gNJyvoiOj/3DgRcIWz9yJNkze8lnutMOzxobg/o2i9oewa2MJk+MHKUZOOCx
oaVfmdczTqDIXdowxnWCTEgWb4SBN+MHGu+8pWgGqXCioGDPALHRR98CWopHC0z7
Via/UXkLNGCjJfdNZiJFnLHG8tATDvDSCDQSg46MARk5Ein4ekVPaNKnjc6INnO0
1QIDAQAB
-----END PUBLIC KEY-----


This is the public key.  I need to now use my script 

```
import jwt
import requests

r = requests.get('https://web.cryptohack.org/rsa-or-hmac/get_pubkey/')
public_key_pem = r.json()["pubkey"].encode()

token = jwt.encode({'username': 'admin', 'admin': True}, public_key_pem, algorithm='HS256')

print(token)
```

In order to sign the HS256 token with the public key. 

Now after i got the public key I realize that this begins with

-----BEGIN PUBLIC KEY----- not

-----BEGIN RSA PUBLIC KEY-----


Steps to reproduce

1. Get Two Tokens from the website and run it through https://github.com/FlorianPicca/JWT-Key-Recovery to get the public key
2. Put public key into file and change
3. Run dis 