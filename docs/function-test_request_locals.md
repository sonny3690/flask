



# test_request_locals()
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=0ff71391f1e7a913b5de
```
def test_request_locals():
    assert repr(flask.g) == "<LocalProxy unbound>"
    assert not flask.g
```  
+++

\
