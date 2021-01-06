



# test_request_processing(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=7a2ce19474b7c4b7cf0b
```
def test_request_processing(app, client):
    evts = []

    @app.before_request
    def before_request():
        evts.append("before")

    @app.after_request
    def after_request(response):
        response.data += b"|after"
        evts.append("after")
        return response

    @app.route("/")
    def index():
        assert "before" in evts
        assert "after" not in evts
        return "request"

    assert "after" not in evts
    rv = client.get("/").data
    assert "after" in evts
    assert rv == b"request|after"
```  
+++

\
