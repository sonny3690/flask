



# test_inject_blueprint_url_defaults(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=c921c011c8066d3761c2
```
def test_inject_blueprint_url_defaults(app):
    bp = flask.Blueprint("foo.bar.baz", __name__, template_folder="template")

    @bp.url_defaults
    def bp_defaults(endpoint, values):
        values["page"] = "login"

    @bp.route("/<page>")
    def view(page):
        pass

    app.register_blueprint(bp)

    values = dict()
    app.inject_url_defaults("foo.bar.baz.view", values)
    expected = dict(page="login")
    assert values == expected

    with app.test_request_context("/somepage"):
        url = flask.url_for("foo.bar.baz.view")
    expected = "/login"
    assert url == expected
```  
+++

\
