



# test_before_first_request_functions_concurrent(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=4d7034c07f656e1a86d6
```
def test_before_first_request_functions_concurrent(app, client):
    got = []

    @app.before_first_request
    def foo():
        time.sleep(0.2)
        got.append(42)

    def get_and_assert():
        client.get("/")
        assert got == [42]

    t = Thread(target=get_and_assert)
    t.start()
    get_and_assert()
    t.join()
    assert app.got_first_request
```  
+++

\
