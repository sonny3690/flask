



# test_extended_flashing(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=b210b31950b72230c34d
```
def test_extended_flashing(app):
    # Be sure app.testing=True below, else tests can fail silently.
    #
    # Specifically, if app.testing is not set to True, the AssertionErrors
    # in the view functions will cause a 500 response to the test client
    # instead of propagating exceptions.

    @app.route("/")
    def index():
        flask.flash("Hello World")
        flask.flash("Hello World", "error")
        flask.flash(flask.Markup("<em>Testing</em>"), "warning")
        return ""

    @app.route("/test/")
    def test():
        messages = flask.get_flashed_messages()
        assert list(messages) == [
            "Hello World",
            "Hello World",
            flask.Markup("<em>Testing</em>"),
        ]
        return ""

    @app.route("/test_with_categories/")
    def test_with_categories():
        messages = flask.get_flashed_messages(with_categories=True)
        assert len(messages) == 3
        assert list(messages) == [
            ("message", "Hello World"),
            ("error", "Hello World"),
            ("warning", flask.Markup("<em>Testing</em>")),
        ]
        return ""

    @app.route("/test_filter/")
    def test_filter():
        messages = flask.get_flashed_messages(
            category_filter=["message"], with_categories=True
        )
        assert list(messages) == [("message", "Hello World")]
        return ""

    @app.route("/test_filters/")
    def test_filters():
        messages = flask.get_flashed_messages(
            category_filter=["message", "warning"], with_categories=True
        )
        assert list(messages) == [
            ("message", "Hello World"),
            ("warning", flask.Markup("<em>Testing</em>")),
        ]
        return ""

    @app.route("/test_filters_without_returning_categories/")
    def test_filters2():
        messages = flask.get_flashed_messages(category_filter=["message", "warning"])
        assert len(messages) == 2
        assert messages[0] == "Hello World"
        assert messages[1] == flask.Markup("<em>Testing</em>")
        return ""

    # Create new test client on each test to clean flashed messages.

    client = app.test_client()
    client.get("/")
    client.get("/test_with_categories/")

    client = app.test_client()
    client.get("/")
    client.get("/test_filter/")

    client = app.test_client()
    client.get("/")
    client.get("/test_filters/")

    client = app.test_client()
    client.get("/")
    client.get("/test_filters_without_returning_categories/")
```  
+++

\
