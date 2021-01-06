



# test_g_iteration_protocol(app_ctx)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=1a5f179a14d42c36bba0
```
def test_g_iteration_protocol(app_ctx):
    flask.g.foo = 23
    flask.g.bar = 42
    assert "foo" in flask.g
    assert "foos" not in flask.g
    assert sorted(flask.g) == ["bar", "foo"]
```  
+++

\
