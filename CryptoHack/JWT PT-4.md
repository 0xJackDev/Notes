
We've explored how flawed verification can break the security of JWTs, but it can sometimes be possible to exploit the code to sign unexpected data in the first place.


```
import json
import jwt # note this is the PyJWT module, not python-jwt


FLAG = ?
SECRET_KEY = ?


@chal.route('/json-in-json/authorise/<token>/')
def authorise(token):
    try:
        decoded = jwt.decode(token, SECRET_KEY, algorithms=['HS256'])
    except Exception as e:
        return {"error": str(e)}

    if "admin" in decoded and decoded["admin"] == "True":
        return {"response": f"Welcome admin, here is your flag: {FLAG}"}
    elif "username" in decoded:
        return {"response": f"Welcome {decoded['username']}"}
    else:
        return {"error": "There is something wrong with your session, goodbye"}


@chal.route('/json-in-json/create_session/<username>/')
def create_session(username):
    body = '{' \
              + '"admin": "' + "False" \
              + '", "username": "' + str(username) \
              + '"}'
    encoded = jwt.encode(json.loads(body), SECRET_KEY, algorithm='HS256')
    return {"session": encoded}
```



The vuln here appears in the second endpoint create_session. 

Notice something here. 
```
    body = '{' \
              + '"admin": "' + "False" \
              + '", "username": "' + str(username) \
              + '"}'
```

This is created in valid JSON format. 

We then do this json.loads(body) turning the data into JSON again even though it was already JSON. Leading to double JSON inside of JSON. 

https://www.invicti.com/learn/json-injection/

So lets say a attacker sends 
hacker", "admin": "True

to the create_session 

https://owasp.org/www-community/Injection_Theory

the reason my payload works is when its first plugged in its 

{
  "admin": "False", "username": "hacker", "admin": "True"
}

Then it is passed into json.loads and becomes 

{
  "admin": "True",
  "username": "hacker"
}

This is because the second key wins in python as it goes like

admin = False 
username = hacker
admin = True. 

Then puts the values of these keys back into a dict. Overwritting the false value to true and leaving

{
  "admin": "True",
  "username": "hacker"
}


