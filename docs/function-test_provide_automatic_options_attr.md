



# test_provide_automatic_options_attr()
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=89899063764f59b60144
```
def test_provide_automatic_options_attr():
    app = flask.Flask(__name__)

    def index():
        return "Hello World!"

    index.provide_automatic_options = False
    app.route("/")(index)
    rv = app.test_client().open("/", method="OPTIONS")
    assert rv.status_code == 405

    app = flask.Flask(__name__)

    def index2():
        return "Hello World!"

    index2.provide_automatic_options = True
    app.route("/", methods=["OPTIONS"])(index2)
    rv = app.test_client().open("/", method="OPTIONS")
    assert sorted(rv.allow) == ["OPTIONS"]
```  
+++

\
