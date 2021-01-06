



# test_url_mapping(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=9e430c59abe6906f3251
```
def test_url_mapping(app, client):
    random_uuid4 = "7eb41166-9ebf-4d26-b771-ea3f54f8b383"

    def index():
        return flask.request.method

    def more():
        return flask.request.method

    def options():
        return random_uuid4

    app.add_url_rule("/", "index", index)
    app.add_url_rule("/more", "more", more, methods=["GET", "POST"])

    # Issue 1288: Test that automatic options are not added
    #             when non-uppercase 'options' in methods
    app.add_url_rule("/options", "options", options, methods=["options"])

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
    rv = client.open("/options", method="OPTIONS")
    assert rv.status_code == 200
    assert random_uuid4 in rv.data.decode("utf-8")
```  
+++

\
