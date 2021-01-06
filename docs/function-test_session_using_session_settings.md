



# test_session_using_session_settings(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=4e27b1327a4d38e0daf6
```
def test_session_using_session_settings(app, client):
    app.config.update(
        SERVER_NAME="www.example.com:8080",
        APPLICATION_ROOT="/test",
        SESSION_COOKIE_DOMAIN=".example.com",
        SESSION_COOKIE_HTTPONLY=False,
        SESSION_COOKIE_SECURE=True,
        SESSION_COOKIE_SAMESITE="Lax",
        SESSION_COOKIE_PATH="/",
    )

    @app.route("/")
    def index():
        flask.session["testing"] = 42
        return "Hello World"

    rv = client.get("/", "http://www.example.com:8080/test/")
    cookie = rv.headers["set-cookie"].lower()
    assert "domain=.example.com" in cookie
    assert "path=/" in cookie
    assert "secure" in cookie
    assert "httponly" not in cookie
    assert "samesite" in cookie
```  
+++

\
