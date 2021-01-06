



# test_baseexception_error_handling(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=51861757f44ef7240599
```
def test_baseexception_error_handling(app, client):
    app.testing = False

    @app.route("/")
    def broken_func():
        raise KeyboardInterrupt()

    with pytest.raises(KeyboardInterrupt):
        client.get("/")

        ctx = flask._request_ctx_stack.top
        assert ctx.preserved
        assert type(ctx._preserved_exc) is KeyboardInterrupt
```  
+++

\
