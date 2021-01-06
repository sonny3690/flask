



# test_after_request_processing(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=26094c6b338f9f27b4ac
```
def test_after_request_processing(app, client):
    @app.route("/")
    def index():
        @flask.after_this_request
        def foo(response):
            response.headers["X-Foo"] = "a header"
            return response

        return "Test"

    resp = client.get("/")
    assert resp.status_code == 200
    assert resp.headers["X-Foo"] == "a header"
```  
+++

\
