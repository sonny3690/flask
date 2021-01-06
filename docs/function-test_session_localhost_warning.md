



# test_session_localhost_warning(recwarn, app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=24a2a99007319851d6f1
```
def test_session_localhost_warning(recwarn, app, client):
    app.config.update(SERVER_NAME="localhost:5000")

    @app.route("/")
    def index():
        flask.session["testing"] = 42
        return "testing"

    rv = client.get("/", "http://localhost:5000/")
    assert "domain" not in rv.headers["set-cookie"].lower()
    w = recwarn.pop(UserWarning)
    assert "'localhost' is not a valid cookie domain" in str(w.message)
```  
+++

\
