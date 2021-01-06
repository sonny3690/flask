



# test_flashes(app, req_ctx)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=da413527bf66a3cce680
```
def test_flashes(app, req_ctx):
    assert not flask.session.modified
    flask.flash("Zap")
    flask.session.modified = False
    flask.flash("Zip")
    assert flask.session.modified
    assert list(flask.get_flashed_messages()) == ["Zap", "Zip"]
```  
+++

\
