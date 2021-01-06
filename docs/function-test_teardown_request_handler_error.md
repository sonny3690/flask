



# test_teardown_request_handler_error(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=95c676e5f961852e3345
```
def test_teardown_request_handler_error(app, client):
    called = []
    app.testing = False

    @app.teardown_request
    def teardown_request1(exc):
        assert type(exc) == ZeroDivisionError
        called.append(True)
        # This raises a new error and blows away sys.exc_info(), so we can
        # test that all teardown_requests get passed the same original
        # exception.
        try:
            raise TypeError()
        except Exception:
            pass

    @app.teardown_request
    def teardown_request2(exc):
        assert type(exc) == ZeroDivisionError
        called.append(True)
        # This raises a new error and blows away sys.exc_info(), so we can
        # test that all teardown_requests get passed the same original
        # exception.
        try:
            raise TypeError()
        except Exception:
            pass

    @app.route("/")
    def fails():
        1 // 0

    rv = client.get("/")
    assert rv.status_code == 500
    assert b"Internal Server Error" in rv.data
    assert len(called) == 2
```  
+++

\
