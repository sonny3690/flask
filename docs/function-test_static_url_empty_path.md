



# test_static_url_empty_path(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=017a5502769dc9f49fde
```
def test_static_url_empty_path(app):
    app = flask.Flask(__name__, static_folder="", static_url_path="")
    rv = app.test_client().open("/static/index.html", method="GET")
    assert rv.status_code == 200
    rv.close()
```  
+++

\
