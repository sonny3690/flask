



# test_subdomain_matching()
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=030be9535db56cb3c2e3
```
def test_subdomain_matching():
    app = flask.Flask(__name__, subdomain_matching=True)
    client = app.test_client()
    app.config["SERVER_NAME"] = "localhost.localdomain"

    @app.route("/", subdomain="<user>")
    def index(user):
        return f"index for {user}"

    rv = client.get("/", "http://mitsuhiko.localhost.localdomain/")
    assert rv.data == b"index for mitsuhiko"
```  
+++

\
