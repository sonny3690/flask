



# test_session_using_server_name(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=7c490cdb337cc4da40d2
```
def test_session_using_server_name(app, client):
    app.config.update(SERVER_NAME="example.com")

    @app.route("/")
    def index():
        flask.session["testing"] = 42
        return "Hello World"

    rv = client.get("/", "http://example.com/")
    assert "domain=.example.com" in rv.headers["set-cookie"].lower()
    assert "httponly" in rv.headers["set-cookie"].lower()
```  
+++

\
