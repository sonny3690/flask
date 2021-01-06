



# test_jsonify_no_prettyprint(app, req_ctx)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=8ec3eaae003bf2b7c6e7
```
def test_jsonify_no_prettyprint(app, req_ctx):
    app.config.update({"JSONIFY_PRETTYPRINT_REGULAR": False})
    compressed_msg = b'{"msg":{"submsg":"W00t"},"msg2":"foobar"}\n'
    uncompressed_msg = {"msg": {"submsg": "W00t"}, "msg2": "foobar"}

    rv = flask.make_response(flask.jsonify(uncompressed_msg), 200)
    assert rv.data == compressed_msg
```  
+++

\
