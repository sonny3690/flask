



# test_request_dispatching(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=50318f20a1bd613b2268
```
def test_request_dispatching(app, client):
    @app.route("/")
    def index():
        return flask.request.method

    @app.route("/more", methods=["GET", "POST"])
    def more():
        return flask.request.method

    assert client.get("/").data == b"GET"
    rv = client.post("/")
    assert rv.status_code == 405
    assert sorted(rv.allow) == ["GET", "HEAD", "OPTIONS"]
    rv = client.head("/")
    assert rv.status_code == 200
    assert not rv.data  # head truncates
    assert client.post("/more").data == b"POST"
    assert client.get("/more").data == b"GET"
    rv = client.delete("/more")
    assert rv.status_code == 405
    assert sorted(rv.allow) == ["GET", "HEAD", "OPTIONS", "POST"]
```  
+++

\
