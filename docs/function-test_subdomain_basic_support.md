



# test_subdomain_basic_support()
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=478ca5488baee4689860
```
def test_subdomain_basic_support():
    app = flask.Flask(__name__, subdomain_matching=True)
    app.config["SERVER_NAME"] = "localhost.localdomain"
    client = app.test_client()

    @app.route("/")
    def normal_index():
        return "normal index"

    @app.route("/", subdomain="test")
    def test_index():
        return "test index"

    rv = client.get("/", "http://localhost.localdomain/")
    assert rv.data == b"normal index"

    rv = client.get("/", "http://test.localhost.localdomain/")
    assert rv.data == b"test index"
```  
+++

\
