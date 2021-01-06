



# test_disallow_string_for_allowed_methods(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=3e7ffaee4eb7edb41042
```
def test_disallow_string_for_allowed_methods(app):
    with pytest.raises(TypeError):

        @app.route("/", methods="GET POST")
        def index():
            return "Hey"
```  
+++

\
