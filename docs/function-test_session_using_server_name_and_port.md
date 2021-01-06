



# test_session_using_server_name_and_port(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=da2f915ba729ca629a77
```
def test_session_using_server_name_and_port(app, client):
    app.config.update(SERVER_NAME="example.com:8080")

    @app.route("/")
    def index():
        flask.session["testing"] = 42
        return "Hello World"

    rv = client.get("/", "http://example.com:8080/")
    assert "domain=.example.com" in rv.headers["set-cookie"].lower()
    assert "httponly" in rv.headers["set-cookie"].lower()
```  
+++

\
