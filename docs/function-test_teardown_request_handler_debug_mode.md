



# test_teardown_request_handler_debug_mode(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=7eedd3630e78eed73b01
```
def test_teardown_request_handler_debug_mode(app, client):
    called = []

    @app.teardown_request
    def teardown_request(exc):
        called.append(True)
        return "Ignored"

    @app.route("/")
    def root():
        return "Response"

    rv = client.get("/")
    assert rv.status_code == 200
    assert b"Response" in rv.data
    assert len(called) == 1
```  
+++

\
