



# test_static_folder_with_ending_slash()
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=eec6888c5fba998e96e6
```
def test_static_folder_with_ending_slash():
    app = flask.Flask(__name__, static_folder="static/")

    @app.route("/<path:path>")
    def catch_all(path):
        return path

    rv = app.test_client().get("/catch/all")
    assert rv.data == b"catch/all"
```  
+++

\
