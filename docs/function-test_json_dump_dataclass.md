



# test_json_dump_dataclass(app, req_ctx)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=8c9bfeda6133b7e45b7e
```
def test_json_dump_dataclass(app, req_ctx):
    from dataclasses import make_dataclass

    Data = make_dataclass("Data", [("name", str)])
    value = flask.json.dumps(Data("Flask"), app=app)
    value = flask.json.loads(value, app=app)
    assert value == {"name": "Flask"}
```  
+++

\
