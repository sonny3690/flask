



# test_session_ip_warning(recwarn, app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=238bac80af5bfa4b5c3c
```
def test_session_ip_warning(recwarn, app, client):
    app.config.update(SERVER_NAME="127.0.0.1:5000")

    @app.route("/")
    def index():
        flask.session["testing"] = 42
        return "testing"

    rv = client.get("/", "http://127.0.0.1:5000/")
    assert "domain=127.0.0.1" in rv.headers["set-cookie"].lower()
    w = recwarn.pop(UserWarning)
    assert "cookie domain is an IP" in str(w.message)
```  
+++

\
