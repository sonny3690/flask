



# test_options_work(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=ed56c22d142e9100fec2
```
def test_options_work(app, client):
    @app.route("/", methods=["GET", "POST"])
    def index():
        return "Hello World"

    rv = client.open("/", method="OPTIONS")
    assert sorted(rv.allow) == ["GET", "HEAD", "OPTIONS", "POST"]
    assert rv.data == b""
```  
+++

\
