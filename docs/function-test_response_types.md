



# test_response_types(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=5889912d10eb45ae30f7
```
def test_response_types(app, client):
    @app.route("/text")
    def from_text():
        return "Hällo Wörld"

    @app.route("/bytes")
    def from_bytes():
        return "Hällo Wörld".encode()

    @app.route("/full_tuple")
    def from_full_tuple():
        return (
            "Meh",
            400,
            {"X-Foo": "Testing", "Content-Type": "text/plain; charset=utf-8"},
        )

    @app.route("/text_headers")
    def from_text_headers():
        return "Hello", {"X-Foo": "Test", "Content-Type": "text/plain; charset=utf-8"}

    @app.route("/text_status")
    def from_text_status():
        return "Hi, status!", 400

    @app.route("/response_headers")
    def from_response_headers():
        return (
            flask.Response(
                "Hello world", 404, {"Content-Type": "text/html", "X-Foo": "Baz"}
            ),
            {"Content-Type": "text/plain", "X-Foo": "Bar", "X-Bar": "Foo"},
        )

    @app.route("/response_status")
    def from_response_status():
        return app.response_class("Hello world", 400), 500

    @app.route("/wsgi")
    def from_wsgi():
        return NotFound()

    @app.route("/dict")
    def from_dict():
        return {"foo": "bar"}, 201

    assert client.get("/text").data == "Hällo Wörld".encode()
    assert client.get("/bytes").data == "Hällo Wörld".encode()

    rv = client.get("/full_tuple")
    assert rv.data == b"Meh"
    assert rv.headers["X-Foo"] == "Testing"
    assert rv.status_code == 400
    assert rv.mimetype == "text/plain"

    rv = client.get("/text_headers")
    assert rv.data == b"Hello"
    assert rv.headers["X-Foo"] == "Test"
    assert rv.status_code == 200
    assert rv.mimetype == "text/plain"

    rv = client.get("/text_status")
    assert rv.data == b"Hi, status!"
    assert rv.status_code == 400
    assert rv.mimetype == "text/html"

    rv = client.get("/response_headers")
    assert rv.data == b"Hello world"
    assert rv.content_type == "text/plain"
    assert rv.headers.getlist("X-Foo") == ["Bar"]
    assert rv.headers["X-Bar"] == "Foo"
    assert rv.status_code == 404

    rv = client.get("/response_status")
    assert rv.data == b"Hello world"
    assert rv.status_code == 500

    rv = client.get("/wsgi")
    assert b"Not Found" in rv.data
    assert rv.status_code == 404

    rv = client.get("/dict")
    assert rv.json == {"foo": "bar"}
    assert rv.status_code == 201
```  
+++

\
