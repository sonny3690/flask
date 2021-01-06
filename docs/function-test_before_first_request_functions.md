



# test_before_first_request_functions(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=b5b1e0e482df8c82cc22
```
def test_before_first_request_functions(app, client):
    got = []

    @app.before_first_request
    def foo():
        got.append(42)

    client.get("/")
    assert got == [42]
    client.get("/")
    assert got == [42]
    assert app.got_first_request
```  
+++

\
