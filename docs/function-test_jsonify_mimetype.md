



# test_jsonify_mimetype(app, req_ctx)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=6175cc8c7a5517f64f25
```
def test_jsonify_mimetype(app, req_ctx):
    app.config.update({"JSONIFY_MIMETYPE": "application/vnd.api+json"})
    msg = {"msg": {"submsg": "W00t"}}
    rv = flask.make_response(flask.jsonify(msg), 200)
    assert rv.mimetype == "application/vnd.api+json"
```  
+++

\
