



# test_build_error_handler_reraise(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=17b519f260e8df193a6e
```
def test_build_error_handler_reraise(app):
    # Test a custom handler which reraises the BuildError
    def handler_raises_build_error(error, endpoint, values):
        raise error

    app.url_build_error_handlers.append(handler_raises_build_error)

    with app.test_request_context():
        pytest.raises(BuildError, flask.url_for, "not.existing")
```  
+++

\
