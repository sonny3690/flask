



# test_session_stored_last(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=623a0303c5cb776bef4d
```
def test_session_stored_last(app, client):
    @app.after_request
    def modify_session(response):
        flask.session["foo"] = 42
        return response

    @app.route("/")
    def dump_session_contents():
        return repr(flask.session.get("foo"))

    assert client.get("/").data == b"None"
    assert client.get("/").data == b"42"
```  
+++

\
