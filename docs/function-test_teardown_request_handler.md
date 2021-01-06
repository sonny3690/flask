



# test_teardown_request_handler(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=441824b8b7ba1e0d952e
```
def test_teardown_request_handler(app, client):
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
