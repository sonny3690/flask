



# test_before_after_request_order(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=65df6405fd0cf912e80a
```
def test_before_after_request_order(app, client):
    called = []

    @app.before_request
    def before1():
        called.append(1)

    @app.before_request
    def before2():
        called.append(2)

    @app.after_request
    def after1(response):
        called.append(4)
        return response

    @app.after_request
    def after2(response):
        called.append(3)
        return response

    @app.teardown_request
    def finish1(exc):
        called.append(6)

    @app.teardown_request
    def finish2(exc):
        called.append(5)

    @app.route("/")
    def index():
        return "42"

    rv = client.get("/")
    assert rv.data == b"42"
    assert called == [1, 2, 3, 4, 5, 6]
```  
+++

\
