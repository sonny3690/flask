



# test_get_method_on_g(app_ctx)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=24bbc15dd578630897fa
```
def test_get_method_on_g(app_ctx):
    assert flask.g.get("x") is None
    assert flask.g.get("x", 11) == 11
    flask.g.x = 42
    assert flask.g.get("x") == 42
    assert flask.g.x == 42
```  
+++

\
