



# test_app_freed_on_zero_refcount()
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=c96975291188af7fd7bc
```
def test_app_freed_on_zero_refcount():
    # A Flask instance should not create a reference cycle that prevents CPython
    # from freeing it when all external references to it are released (see #3761).
    gc.disable()
    try:
        app = flask.Flask(__name__)
        assert app.view_functions["static"]
        weak = weakref.ref(app)
        assert weak() is not None
        del app
        assert weak() is None
    finally:
        gc.enable()
```  
+++

\
