



# test_jsonify_args_and_kwargs_check(app, req_ctx)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=bab690f3a9142f7c1639
```
def test_jsonify_args_and_kwargs_check(app, req_ctx):
    with pytest.raises(TypeError) as e:
        flask.jsonify("fake args", kwargs="fake")
    assert "behavior undefined" in str(e.value)
```  
+++

\
