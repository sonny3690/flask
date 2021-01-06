



# test_session_using_application_root(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=df9a87fa07f0f9c3fb23
```
def test_session_using_application_root(app, client):
    class PrefixPathMiddleware:
        def __init__(self, app, prefix):
            self.app = app
            self.prefix = prefix

        def __call__(self, environ, start_response):
            environ["SCRIPT_NAME"] = self.prefix
            return self.app(environ, start_response)

    app.wsgi_app = PrefixPathMiddleware(app.wsgi_app, "/bar")
    app.config.update(APPLICATION_ROOT="/bar")

    @app.route("/")
    def index():
        flask.session["testing"] = 42
        return "Hello World"

    rv = client.get("/", "http://example.com:8080/")
    assert "path=/bar" in rv.headers["set-cookie"].lower()
```  
+++

\
