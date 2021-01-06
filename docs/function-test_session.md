



# test_session(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=c350a97c607cf0b78d09
```
def test_session(app, client):
    @app.route("/set", methods=["POST"])
    def set():
        assert not flask.session.accessed
        assert not flask.session.modified
        flask.session["value"] = flask.request.form["value"]
        assert flask.session.accessed
        assert flask.session.modified
        return "value set"

    @app.route("/get")
    def get():
        assert not flask.session.accessed
        assert not flask.session.modified
        v = flask.session.get("value", "None")
        assert flask.session.accessed
        assert not flask.session.modified
        return v

    assert client.post("/set", data={"value": "42"}).data == b"value set"
    assert client.get("/get").data == b"42"
```  
+++

\
