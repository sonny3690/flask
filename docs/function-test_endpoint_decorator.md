



# test_endpoint_decorator(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=828e30342fe0173540f5
```
def test_endpoint_decorator(app, client):
    from werkzeug.routing import Submount, Rule

    app.url_map.add(
        Submount("/foo", [Rule("/bar", endpoint="bar"), Rule("/", endpoint="index")])
    )

    @app.endpoint("bar")
    def bar():
        return "bar"

    @app.endpoint("index")
    def index():
        return "index"

    assert client.get("/foo/").data == b"index"
    assert client.get("/foo/bar").data == b"bar"
```  
+++

\
