



# test_url_processors(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=5fd52bc2bad1aab54bdd
```
def test_url_processors(app, client):
    @app.url_defaults
    def add_language_code(endpoint, values):
        if flask.g.lang_code is not None and app.url_map.is_endpoint_expecting(
            endpoint, "lang_code"
        ):
            values.setdefault("lang_code", flask.g.lang_code)

    @app.url_value_preprocessor
    def pull_lang_code(endpoint, values):
        flask.g.lang_code = values.pop("lang_code", None)

    @app.route("/<lang_code>/")
    def index():
        return flask.url_for("about")

    @app.route("/<lang_code>/about")
    def about():
        return flask.url_for("something_else")

    @app.route("/foo")
    def something_else():
        return flask.url_for("about", lang_code="en")

    assert client.get("/de/").data == b"/de/about"
    assert client.get("/de/about").data == b"/foo"
    assert client.get("/foo").data == b"/en/about"
```  
+++

\
