



# test_preserve_only_once(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=1acff6b663705e539a93
```
def test_preserve_only_once(app, client):
    app.debug = True

    @app.route("/fail")
    def fail_func():
        1 // 0

    for _x in range(3):
        with pytest.raises(ZeroDivisionError):
            client.get("/fail")

    assert flask._request_ctx_stack.top is not None
    assert flask._app_ctx_stack.top is not None
    # implicit appctx disappears too
    flask._request_ctx_stack.top.pop()
    assert flask._request_ctx_stack.top is None
    assert flask._app_ctx_stack.top is None
```  
+++

\
