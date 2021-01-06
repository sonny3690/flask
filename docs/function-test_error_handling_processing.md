



# test_error_handling_processing(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=74e237ea448775aa7d5a
```
def test_error_handling_processing(app, client):
    app.testing = False

    @app.errorhandler(500)
    def internal_server_error(e):
        return "internal server error", 500

    @app.route("/")
    def broken_func():
        1 // 0

    @app.after_request
    def after_request(resp):
        resp.mimetype = "text/x-special"
        return resp

    resp = client.get("/")
    assert resp.mimetype == "text/x-special"
    assert resp.data == b"internal server error"
```  
+++

\
