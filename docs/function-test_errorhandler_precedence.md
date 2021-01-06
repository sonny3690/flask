



# test_errorhandler_precedence(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=91527094187e1f8a0ff5
```
def test_errorhandler_precedence(app, client):
    class E1(Exception):
        pass

    class E2(Exception):
        pass

    class E3(E1, E2):
        pass

    @app.errorhandler(E2)
    def handle_e2(e):
        return "E2"

    @app.errorhandler(Exception)
    def handle_exception(e):
        return "Exception"

    @app.route("/E1")
    def raise_e1():
        raise E1

    @app.route("/E3")
    def raise_e3():
        raise E3

    rv = client.get("/E1")
    assert rv.data == b"Exception"

    rv = client.get("/E3")
    assert rv.data == b"E2"
```  
+++

\
