



# test_routing_redirect_debugging(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=96fef5191c8e90c623e9
```
def test_routing_redirect_debugging(app, client):
    app.debug = True

    @app.route("/foo/", methods=["GET", "POST"])
    def foo():
        return "success"

    with client:
        with pytest.raises(AssertionError) as e:
            client.post("/foo", data={})
        assert "http://localhost/foo/" in str(e.value)
        assert "Make sure to directly send your POST-request to this URL" in str(
            e.value
        )

        rv = client.get("/foo", data={}, follow_redirects=True)
        assert rv.data == b"success"

    app.debug = False
    with client:
        rv = client.post("/foo", data={}, follow_redirects=True)
        assert rv.data == b"success"
```  
+++

\
