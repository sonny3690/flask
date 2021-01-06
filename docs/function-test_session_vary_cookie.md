



# test_session_vary_cookie(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=ef9bb293091f96e6823d
```
def test_session_vary_cookie(app, client):
    @app.route("/set")
    def set_session():
        flask.session["test"] = "test"
        return ""

    @app.route("/get")
    def get():
        return flask.session.get("test")

    @app.route("/getitem")
    def getitem():
        return flask.session["test"]

    @app.route("/setdefault")
    def setdefault():
        return flask.session.setdefault("test", "default")

    @app.route("/vary-cookie-header-set")
    def vary_cookie_header_set():
        response = flask.Response()
        response.vary.add("Cookie")
        flask.session["test"] = "test"
        return response

    @app.route("/vary-header-set")
    def vary_header_set():
        response = flask.Response()
        response.vary.update(("Accept-Encoding", "Accept-Language"))
        flask.session["test"] = "test"
        return response

    @app.route("/no-vary-header")
    def no_vary_header():
        return ""

    def expect(path, header_value="Cookie"):
        rv = client.get(path)

        if header_value:
            # The 'Vary' key should exist in the headers only once.
            assert len(rv.headers.get_all("Vary")) == 1
            assert rv.headers["Vary"] == header_value
        else:
            assert "Vary" not in rv.headers

    expect("/set")
    expect("/get")
    expect("/getitem")
    expect("/setdefault")
    expect("/vary-cookie-header-set")
    expect("/vary-header-set", "Accept-Encoding, Accept-Language, Cookie")
    expect("/no-vary-header", None)
```  
+++

\
