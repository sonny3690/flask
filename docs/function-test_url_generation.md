



# test_url_generation(app, req_ctx)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=1790ba37a566f7d07d28
```
def test_url_generation(app, req_ctx):
    @app.route("/hello/<name>", methods=["POST"])
    def hello():
        pass

    assert flask.url_for("hello", name="test x") == "/hello/test%20x"
    assert (
        flask.url_for("hello", name="test x", _external=True)
        == "http://localhost/hello/test%20x"
    )
```  
+++

\
