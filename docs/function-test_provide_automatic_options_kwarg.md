



# test_provide_automatic_options_kwarg(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=aa508e3fcc513edf3b43
```
def test_provide_automatic_options_kwarg(app, client):
    def index():
        return flask.request.method

    def more():
        return flask.request.method

    app.add_url_rule("/", view_func=index, provide_automatic_options=False)
    app.add_url_rule(
        "/more",
        view_func=more,
        methods=["GET", "POST"],
        provide_automatic_options=False,
    )
    assert client.get("/").data == b"GET"

    rv = client.post("/")
    assert rv.status_code == 405
    assert sorted(rv.allow) == ["GET", "HEAD"]

    rv = client.open("/", method="OPTIONS")
    assert rv.status_code == 405

    rv = client.head("/")
    assert rv.status_code == 200
    assert not rv.data  # head truncates
    assert client.post("/more").data == b"POST"
    assert client.get("/more").data == b"GET"

    rv = client.delete("/more")
    assert rv.status_code == 405
    assert sorted(rv.allow) == ["GET", "HEAD", "POST"]

    rv = client.open("/more", method="OPTIONS")
    assert rv.status_code == 405
```  
+++

\
