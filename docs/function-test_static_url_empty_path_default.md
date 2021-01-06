



# test_static_url_empty_path_default(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=4c70f15155c56d99bd85
```
def test_static_url_empty_path_default(app):
    app = flask.Flask(__name__, static_folder="")
    rv = app.test_client().open("/static/index.html", method="GET")
    assert rv.status_code == 200
    rv.close()
```  
+++

\
