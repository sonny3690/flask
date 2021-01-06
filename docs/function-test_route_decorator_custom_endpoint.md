



# test_route_decorator_custom_endpoint(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=cd2db97a110d1de42224
```
def test_route_decorator_custom_endpoint(app, client):
    app.debug = True

    @app.route("/foo/")
    def foo():
        return flask.request.endpoint

    @app.route("/bar/", endpoint="bar")
    def for_bar():
        return flask.request.endpoint

    @app.route("/bar/123", endpoint="123")
    def for_bar_foo():
        return flask.request.endpoint

    with app.test_request_context():
        assert flask.url_for("foo") == "/foo/"
        assert flask.url_for("bar") == "/bar/"
        assert flask.url_for("123") == "/bar/123"

    assert client.get("/foo/").data == b"foo"
    assert client.get("/bar/").data == b"bar"
    assert client.get("/bar/123").data == b"123"
```  
+++

\
