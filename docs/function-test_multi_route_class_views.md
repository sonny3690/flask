



# test_multi_route_class_views(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=5b51514649375a8d9aa2
```
def test_multi_route_class_views(app, client):
    class View:
        def __init__(self, app):
            app.add_url_rule("/", "index", self.index)
            app.add_url_rule("/<test>/", "index", self.index)

        def index(self, test="a"):
            return test

    _ = View(app)
    rv = client.open("/")
    assert rv.data == b"a"
    rv = client.open("/b/")
    assert rv.data == b"b"
```  
+++

\
