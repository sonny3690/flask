



# test_max_content_length(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=d4a4baeb3a29c30d7c80
```
def test_max_content_length(app, client):
    app.config["MAX_CONTENT_LENGTH"] = 64

    @app.before_request
    def always_first():
        flask.request.form["myfile"]
        AssertionError()

    @app.route("/accept", methods=["POST"])
    def accept_file():
        flask.request.form["myfile"]
        AssertionError()

    @app.errorhandler(413)
    def catcher(error):
        return "42"

    rv = client.post("/accept", data={"myfile": "foo" * 100})
    assert rv.data == b"42"
```  
+++

\
