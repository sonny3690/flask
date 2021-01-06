



# test_enctype_debug_helper(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=e1872b12e0449c0ff7ea
```
def test_enctype_debug_helper(app, client):
    from flask.debughelpers import DebugFilesKeyError

    app.debug = True

    @app.route("/fail", methods=["POST"])
    def index():
        return flask.request.files["foo"].filename

    # with statement is important because we leave an exception on the
    # stack otherwise and we want to ensure that this is not the case
    # to not negatively affect other tests.
    with client:
        with pytest.raises(DebugFilesKeyError) as e:
            client.post("/fail", data={"foo": "index.txt"})
        assert "no file contents were transmitted" in str(e.value)
        assert "This was submitted: 'index.txt'" in str(e.value)
```  
+++

\
