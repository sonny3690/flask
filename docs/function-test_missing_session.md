



# test_missing_session(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=79033102c60d100463c6
```
def test_missing_session(app):
    app.secret_key = None

    def expect_exception(f, *args, **kwargs):
        e = pytest.raises(RuntimeError, f, *args, **kwargs)
        assert e.value.args and "session is unavailable" in e.value.args[0]

    with app.test_request_context():
        assert flask.session.get("missing_key") is None
        expect_exception(flask.session.__setitem__, "foo", 42)
        expect_exception(flask.session.pop, "foo")
```  
+++

\
