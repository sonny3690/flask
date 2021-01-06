



# test_werkzeug_routing(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=283c541383de729d12ec
```
def test_werkzeug_routing(app, client):
    from werkzeug.routing import Submount, Rule

    app.url_map.add(
        Submount("/foo", [Rule("/bar", endpoint="bar"), Rule("/", endpoint="index")])
    )

    def bar():
        return "bar"

    def index():
        return "index"

    app.view_functions["bar"] = bar
    app.view_functions["index"] = index

    assert client.get("/foo/").data == b"index"
    assert client.get("/foo/bar").data == b"bar"
```  
+++

\
