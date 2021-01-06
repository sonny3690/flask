



# test_trapping_of_bad_request_key_errors(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=0f8bda04f290ed733225
```
def test_trapping_of_bad_request_key_errors(app, client):
    @app.route("/key")
    def fail():
        flask.request.form["missing_key"]

    @app.route("/abort")
    def allow_abort():
        flask.abort(400)

    rv = client.get("/key")
    assert rv.status_code == 400
    assert b"missing_key" not in rv.data
    rv = client.get("/abort")
    assert rv.status_code == 400

    app.debug = True
    with pytest.raises(KeyError) as e:
        client.get("/key")
    assert e.errisinstance(BadRequest)
    assert "missing_key" in e.value.get_description()
    rv = client.get("/abort")
    assert rv.status_code == 400

    app.debug = False
    app.config["TRAP_BAD_REQUEST_ERRORS"] = True
    with pytest.raises(KeyError):
        client.get("/key")
    with pytest.raises(BadRequest):
        client.get("/abort")
```  
+++

\
