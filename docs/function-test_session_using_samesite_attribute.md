



# test_session_using_samesite_attribute(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=2db2d85d31ff1b754cf1
```
def test_session_using_samesite_attribute(app, client):
    @app.route("/")
    def index():
        flask.session["testing"] = 42
        return "Hello World"

    app.config.update(SESSION_COOKIE_SAMESITE="invalid")

    with pytest.raises(ValueError):
        client.get("/")

    app.config.update(SESSION_COOKIE_SAMESITE=None)
    rv = client.get("/")
    cookie = rv.headers["set-cookie"].lower()
    assert "samesite" not in cookie

    app.config.update(SESSION_COOKIE_SAMESITE="Strict")
    rv = client.get("/")
    cookie = rv.headers["set-cookie"].lower()
    assert "samesite=strict" in cookie

    app.config.update(SESSION_COOKIE_SAMESITE="Lax")
    rv = client.get("/")
    cookie = rv.headers["set-cookie"].lower()
    assert "samesite=lax" in cookie
```  
+++

\
