



# test_static_url_path_with_ending_slash()
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=d2cbbb7197ce2f5703b5
```
def test_static_url_path_with_ending_slash():
    app = flask.Flask(__name__, static_url_path="/foo/")
    app.testing = True
    rv = app.test_client().get("/foo/index.html")
    assert rv.status_code == 200
    rv.close()

    with app.test_request_context():
        assert flask.url_for("static", filename="index.html") == "/foo/index.html"
```  
+++

\
