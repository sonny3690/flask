



# test_static_folder_with_pathlib_path(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=f82a0db3621a458cd6f8
```
def test_static_folder_with_pathlib_path(app):
    from pathlib import Path

    app = flask.Flask(__name__, static_folder=Path("static"))
    rv = app.test_client().open("/static/index.html", method="GET")
    assert rv.status_code == 200
    rv.close()
```  
+++

\
