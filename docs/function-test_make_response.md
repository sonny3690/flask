



# test_make_response(app, req_ctx)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=b237350885470333e60e
```
def test_make_response(app, req_ctx):
    rv = flask.make_response()
    assert rv.status_code == 200
    assert rv.data == b""
    assert rv.mimetype == "text/html"

    rv = flask.make_response("Awesome")
    assert rv.status_code == 200
    assert rv.data == b"Awesome"
    assert rv.mimetype == "text/html"

    rv = flask.make_response("W00t", 404)
    assert rv.status_code == 404
    assert rv.data == b"W00t"
    assert rv.mimetype == "text/html"
```  
+++

\
