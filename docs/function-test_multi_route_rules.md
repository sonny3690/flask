



# test_multi_route_rules(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=32779c3109d27ba66bbc
```
def test_multi_route_rules(app, client):
    @app.route("/")
    @app.route("/<test>/")
    def index(test="a"):
        return test

    rv = client.open("/")
    assert rv.data == b"a"
    rv = client.open("/b/")
    assert rv.data == b"b"
```  
+++

\
