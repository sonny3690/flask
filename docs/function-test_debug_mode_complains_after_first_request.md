



# test_debug_mode_complains_after_first_request(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=b20fcb6175d60f7453c1
```
def test_debug_mode_complains_after_first_request(app, client):
    app.debug = True

    @app.route("/")
    def index():
        return "Awesome"

    assert not app.got_first_request
    assert client.get("/").data == b"Awesome"
    with pytest.raises(AssertionError) as e:

        @app.route("/foo")
        def broken():
            return "Meh"

    assert "A setup function was called" in str(e.value)

    app.debug = False

    @app.route("/foo")
    def working():
        return "Meh"

    assert client.get("/foo").data == b"Meh"
    assert app.got_first_request
```  
+++

\
