



# test_subdomain_matching_with_ports()
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=32f644b251b4e5c77601
```
def test_subdomain_matching_with_ports():
    app = flask.Flask(__name__, subdomain_matching=True)
    app.config["SERVER_NAME"] = "localhost.localdomain:3000"
    client = app.test_client()

    @app.route("/", subdomain="<user>")
    def index(user):
        return f"index for {user}"

    rv = client.get("/", "http://mitsuhiko.localhost.localdomain:3000/")
    assert rv.data == b"index for mitsuhiko"
```  
+++

\
