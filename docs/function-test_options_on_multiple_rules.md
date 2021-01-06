



# test_options_on_multiple_rules(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=f6a350618f6399f37d80
```
def test_options_on_multiple_rules(app, client):
    @app.route("/", methods=["GET", "POST"])
    def index():
        return "Hello World"

    @app.route("/", methods=["PUT"])
    def index_put():
        return "Aha!"

    rv = client.open("/", method="OPTIONS")
    assert sorted(rv.allow) == ["GET", "HEAD", "OPTIONS", "POST", "PUT"]
```  
+++

\
