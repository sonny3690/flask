



# test_trapping_of_all_http_exceptions(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=3074c637595efc666941
```
def test_trapping_of_all_http_exceptions(app, client):
    app.config["TRAP_HTTP_EXCEPTIONS"] = True

    @app.route("/fail")
    def fail():
        flask.abort(404)

    with pytest.raises(NotFound):
        client.get("/fail")
```  
+++

\
