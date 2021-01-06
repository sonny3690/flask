



# test_http_error_subclass_handling(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=24eac4110d14193f0bfc
```
def test_http_error_subclass_handling(app, client):
    class ForbiddenSubclass(Forbidden):
        pass

    @app.errorhandler(ForbiddenSubclass)
    def handle_forbidden_subclass(e):
        assert isinstance(e, ForbiddenSubclass)
        return "banana"

    @app.errorhandler(403)
    def handle_403(e):
        assert not isinstance(e, ForbiddenSubclass)
        assert isinstance(e, Forbidden)
        return "apple"

    @app.route("/1")
    def index1():
        raise ForbiddenSubclass()

    @app.route("/2")
    def index2():
        flask.abort(403)

    @app.route("/3")
    def index3():
        raise Forbidden()

    assert client.get("/1").data == b"banana"
    assert client.get("/2").data == b"apple"
    assert client.get("/3").data == b"apple"
```  
+++

\
