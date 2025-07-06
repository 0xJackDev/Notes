

RSA or HMAC? 


A little about RS256, the Public-private key pair is used where the issuer uses the private key to sign the JWT header and payload, and the recipient uses the corresponding public key to verify the signature.

Ok Now for da hacking code shiii


```
import jwt # note this is the PyJWT module, not python-jwt


# Key generated using: openssl genrsa -out rsa-or-hmac-private.pem 2048
with open('challenge_files/rsa-or-hmac-private.pem', 'rb') as f:
   PRIVATE_KEY = f.read()
with open('challenge_files/rsa-or-hmac-public.pem', 'rb') as f:
   PUBLIC_KEY = f.read()

FLAG = ?


@chal.route('/rsa-or-hmac/authorise/<token>/')
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


@chal.route('/rsa-or-hmac/create_session/<username>/')
def create_session(username):
    encoded = jwt.encode({'username': username, 'admin': False}, PRIVATE_KEY, algorithm='RS256')
    return {"session": encoded}


@chal.route('/rsa-or-hmac/get_pubkey/')
def get_pubkey():
    return {"pubkey": PUBLIC_KEY}
```


What stands out to me is this line 

```
        decoded = jwt.decode(token, PUBLIC_KEY, algorithms=['HS256', 'RS256'])
```

Also about this server

The server is running PyJWT with a small patch to enable an exploit that existed in PyJWT versions <= 1.5.0. To create the malicious signature, you will need to patch your PyJWT library too. If you want to patch, look at the line that was added in the [fix for the vulnerability](https://github.com/jpadilla/pyjwt/commit/37926ea0dd207db070b45473438853447e4c1392). Use `pip show pyjwt` to find the location of the PyJWT library on your computer, and make the edit. For versions of PyJWT > 2.4.0 the code has been changed so you will have to edit `jwt/utils.py` instead of `jwt/algorithms.py`


I found a blog post about this


https://www.vicarius.io/vsociety/posts/risky-algorithms-algorithm-confusion-in-pyjwt-cve-2022-29217


Heres what the Introduction is

# Introduction

Imagine you are the head of the security unit in an organization and the door to the main building requires access cards for entry. This door accepts all access cards like magnetic stripe, proximity, Wiegand, and smart cards. However, allowing the use of all kinds of access cards makes the door vulnerable to attacks because some can be cloned, making the entire building vulnerable to attacks. An attacker could forge any of these weak access cards and gain unauthorized entry to the main building. This is the case of CVE-2022-29217.

This vulnerability affects [PyJWT](https://pypi.org/project/PyJWT/) from version 1.5.0 to version 2.3.0. These vulnerable versions of PyJWT support all algorithms when `jwt.algorithms.get_default_algorithms()` is used during decoding. Algorithms determine the level of security in cryptography and this could be exploited by an attacker. Since all algorithms are supported when `jwt.algorithms.get_default_algorithms()` is used, both asymmetric and symmetric algorithms are supported. An attacker could craft a token using the wrong key and algorithm combination and have the JWT checker verify it as a valid one. For example, an attacker could sign a token using the HMAC algorithm; a symmetric algorithm with a public key, and have the token verified as a valid one using the `jwt.algorithms.get_default_algorithms()` call. This is possible because all algorithm types (asymmetric and symmetric) are supported using that call.


Makes sense kinda not but I think its saying I can generate a HS256 with the public key which is available to me using so I can do the HMAC (Hash-based message authentication code) using the secret as the Public key but it mentions a specific function being passed as a parameter for the algorithms inside of the jwt.decode function the jwt.algorithms.get_default_algorithms()  function. Although since they manually set algorithms=['HS256', 'RS256']) and include HS256 even though they dont use it. I should be able to do this POC.

Here is what they use in this long ahh PoC to encode the jwt with the public key

```
encoded_bad = jwt.encode({"test": 1234}, pub_key_bytes, algorithm="HS256")
```

But instead since we need 

```
{'username': 'admin', 'admin': True}, PUBLIC_KEY_BYTES, algorithm='HS256'
```

But we need to write in the public key bytes this is how they do it in their PoC

```
pub_key_bytes = private_key.public_key().public_bytes(encoding=serialization.Encoding.OpenSSH,format=serialization.PublicFormat.OpenSSH)
```

so 




Steps to generate POC.


Get public_key, translate from PEM format to OpenSSH format. its important for this as above compare the difference between PEM and OpenSSH format but looking at the github commit 
https://github.com/jpadilla/pyjwt/commit/37926ea0dd207db070b45473438853447e4c1392 
You see that             b'-----BEGIN RSA PUBLIC KEY-----', was added as a invalid_string.


1.
Get Public Key 

2.
The server is running PyJWT with a small patch to enable an exploit that existed in PyJWT versions <= 1.5.0. To create the malicious signature, you will need to patch your PyJWT library too. If you want to patch, look at the line that was added in the [fix for the vulnerability](https://github.com/jpadilla/pyjwt/commit/37926ea0dd207db070b45473438853447e4c1392). Use `pip show pyjwt` to find the location of the PyJWT library on your computer, and make the edit. For versions of PyJWT > 2.4.0 the code has been changed so you will have to edit `jwt/utils.py` instead of `jwt/algorithms.py`

Edit algorithms.py and remove the string  '-----BEGIN RSA PUBLIC KEY-----'  from the invalid_strings variable in  class HMACAlgorithm(Algorithm):

```
import jwt
import requests

r = requests.get('https://web.cryptohack.org/rsa-or-hmac/get_pubkey/')
public_key_pem = r.json()["pubkey"].encode()

token = jwt.encode({'username': 'admin', 'admin': True}, public_key_pem, algorithm='HS256')

print(token)
```


ugh this did it.... It wasnt working when it fixed it once i used requests to get the raw json then got the pubkey and used the .encode() method. 

