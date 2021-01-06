



# test_static_files(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=deaaa364bc96df613a04
```
def test_static_files(app, client):
    rv = client.get("/static/index.html")
    assert rv.status_code == 200
    assert rv.data.strip() == b"<h1>Hello World!</h1>"
    with app.test_request_context():
        assert flask.url_for("static", filename="index.html") == "/static/index.html"
    rv.close()
```  
+++

\
