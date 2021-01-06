



# test_jsonify_prettyprint(app, req_ctx)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=63b28f2faf5945eb7b0f
```
def test_jsonify_prettyprint(app, req_ctx):
    app.config.update({"JSONIFY_PRETTYPRINT_REGULAR": True})
    compressed_msg = {"msg": {"submsg": "W00t"}, "msg2": "foobar"}
    pretty_response = (
        b'{\n  "msg": {\n    "submsg": "W00t"\n  }, \n  "msg2": "foobar"\n}\n'
    )

    rv = flask.make_response(flask.jsonify(compressed_msg), 200)
    assert rv.data == pretty_response
```  
+++

\
