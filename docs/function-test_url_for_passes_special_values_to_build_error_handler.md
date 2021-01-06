



# test_url_for_passes_special_values_to_build_error_handler(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=b9219f0326616e54ddab
```
def test_url_for_passes_special_values_to_build_error_handler(app):
    @app.url_build_error_handlers.append
    def handler(error, endpoint, values):
        assert values == {
            "_external": False,
            "_anchor": None,
            "_method": None,
            "_scheme": None,
        }
        return "handled"

    with app.test_request_context():
        flask.url_for("/")
```  
+++

\
