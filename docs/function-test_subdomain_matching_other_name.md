



# test_subdomain_matching_other_name(matching)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=da2c99309ff89893e6ee
```
def test_subdomain_matching_other_name(matching):
    app = flask.Flask(__name__, subdomain_matching=matching)
    app.config["SERVER_NAME"] = "localhost.localdomain:3000"
    client = app.test_client()

    @app.route("/")
    def index():
        return "", 204

    # suppress Werkzeug 0.15 warning about name mismatch
    with pytest.warns(None):
        # ip address can't match name
        rv = client.get("/", "http://127.0.0.1:3000/")
        assert rv.status_code == 404 if matching else 204

    # allow all subdomains if matching is disabled
    rv = client.get("/", "http://www.localhost.localdomain:3000/")
    assert rv.status_code == 404 if matching else 204
```  
+++

\
