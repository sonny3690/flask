



# test_error_handler_unknown_code(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=15cfe1abdd8be40b4488
```
def test_error_handler_unknown_code(app):
    with pytest.raises(KeyError) as exc_info:
        app.register_error_handler(999, lambda e: ("999", 999))

    assert "Use a subclass" in exc_info.value.args[0]
```  
+++

\
