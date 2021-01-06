



# test_before_request_and_routing_errors(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=bd7c5ddac0948a0ac6b3
```
def test_before_request_and_routing_errors(app, client):
    @app.before_request
    def attach_something():
        flask.g.something = "value"

    @app.errorhandler(404)
    def return_something(error):
        return flask.g.something, 404

    rv = client.get("/")
    assert rv.status_code == 404
    assert rv.data == b"value"
```  
+++

\
