



# test_session_using_server_name_port_and_path(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=917db309adcbd71d203f
```
def test_session_using_server_name_port_and_path(app, client):
    app.config.update(SERVER_NAME="example.com:8080", APPLICATION_ROOT="/foo")

    @app.route("/")
    def index():
        flask.session["testing"] = 42
        return "Hello World"

    rv = client.get("/", "http://example.com:8080/foo")
    assert "domain=example.com" in rv.headers["set-cookie"].lower()
    assert "path=/foo" in rv.headers["set-cookie"].lower()
    assert "httponly" in rv.headers["set-cookie"].lower()
```  
+++

\
