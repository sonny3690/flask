



# test_error_handling(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=ecdf14a1d4ad5332e9b9
```
def test_error_handling(app, client):
    app.testing = False

    @app.errorhandler(404)
    def not_found(e):
        return "not found", 404

    @app.errorhandler(500)
    def internal_server_error(e):
        return "internal server error", 500

    @app.errorhandler(Forbidden)
    def forbidden(e):
        return "forbidden", 403

    @app.route("/")
    def index():
        flask.abort(404)

    @app.route("/error")
    def error():
        1 // 0

    @app.route("/forbidden")
    def error2():
        flask.abort(403)

    rv = client.get("/")
    assert rv.status_code == 404
    assert rv.data == b"not found"
    rv = client.get("/error")
    assert rv.status_code == 500
    assert b"internal server error" == rv.data
    rv = client.get("/forbidden")
    assert rv.status_code == 403
    assert b"forbidden" == rv.data
```  
+++

\
