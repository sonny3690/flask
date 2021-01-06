



# test_error_handler_after_processor_error(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=798861df6719e5c89d1c
```
def test_error_handler_after_processor_error(app, client):
    app.testing = False

    @app.before_request
    def before_request():
        if _trigger == "before":
            1 // 0

    @app.after_request
    def after_request(response):
        if _trigger == "after":
            1 // 0
        return response

    @app.route("/")
    def index():
        return "Foo"

    @app.errorhandler(500)
    def internal_server_error(e):
        return "Hello Server Error", 500

    for _trigger in "before", "after":
        rv = client.get("/")
        assert rv.status_code == 500
        assert rv.data == b"Hello Server Error"
```  
+++

\
