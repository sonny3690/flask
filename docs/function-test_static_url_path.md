



# test_static_url_path()
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=d0f79734e274fe4bf530
```
def test_static_url_path():
    app = flask.Flask(__name__, static_url_path="/foo")
    app.testing = True
    rv = app.test_client().get("/foo/index.html")
    assert rv.status_code == 200
    rv.close()

    with app.test_request_context():
        assert flask.url_for("static", filename="index.html") == "/foo/index.html"
```  
+++

\
