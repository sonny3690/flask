



# test_nonascii_pathinfo(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=1ce97840e4d9100eb85d
```
def test_nonascii_pathinfo(app, client):
    @app.route("/киртест")
    def index():
        return "Hello World!"

    rv = client.get("/киртест")
    assert rv.data == b"Hello World!"
```  
+++

\
