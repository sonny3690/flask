



# test_preserve_remembers_exception(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=33f511f503dca12f58f7
```
def test_preserve_remembers_exception(app, client):
    app.debug = True
    errors = []

    @app.route("/fail")
    def fail_func():
        1 // 0

    @app.route("/success")
    def success_func():
        return "Okay"

    @app.teardown_request
    def teardown_handler(exc):
        errors.append(exc)

    # After this failure we did not yet call the teardown handler
    with pytest.raises(ZeroDivisionError):
        client.get("/fail")
    assert errors == []

    # But this request triggers it, and it's an error
    client.get("/success")
    assert len(errors) == 2
    assert isinstance(errors[0], ZeroDivisionError)

    # At this point another request does nothing.
    client.get("/success")
    assert len(errors) == 3
    assert errors[1] is None
```  
+++

\
