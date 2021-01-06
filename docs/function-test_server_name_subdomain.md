



# test_server_name_subdomain()
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=fe560e2f77c0fb5297dd
```
def test_server_name_subdomain():
    app = flask.Flask(__name__, subdomain_matching=True)
    client = app.test_client()

    @app.route("/")
    def index():
        return "default"

    @app.route("/", subdomain="foo")
    def subdomain():
        return "subdomain"

    app.config["SERVER_NAME"] = "dev.local:5000"
    rv = client.get("/")
    assert rv.data == b"default"

    rv = client.get("/", "http://dev.local:5000")
    assert rv.data == b"default"

    rv = client.get("/", "https://dev.local:5000")
    assert rv.data == b"default"

    app.config["SERVER_NAME"] = "dev.local:443"
    rv = client.get("/", "https://dev.local")

    # Werkzeug 1.0 fixes matching https scheme with 443 port
    if rv.status_code != 404:
        assert rv.data == b"default"

    app.config["SERVER_NAME"] = "dev.local"
    rv = client.get("/", "https://dev.local")
    assert rv.data == b"default"

    # suppress Werkzeug 1.0 warning about name mismatch
    with pytest.warns(None):
        rv = client.get("/", "http://foo.localhost")
        assert rv.status_code == 404

    rv = client.get("/", "http://foo.dev.local")
    assert rv.data == b"subdomain"
```  
+++

\
