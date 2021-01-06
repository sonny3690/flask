



# test_session_cookie_setting(app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=b011179466543dc0e1af
```
def test_session_cookie_setting(app):
    is_permanent = True

    @app.route("/bump")
    def bump():
        rv = flask.session["foo"] = flask.session.get("foo", 0) + 1
        flask.session.permanent = is_permanent
        return str(rv)

    @app.route("/read")
    def read():
        return str(flask.session.get("foo", 0))

    def run_test(expect_header):
        with app.test_client() as c:
            assert c.get("/bump").data == b"1"
            assert c.get("/bump").data == b"2"
            assert c.get("/bump").data == b"3"

            rv = c.get("/read")
            set_cookie = rv.headers.get("set-cookie")
            assert (set_cookie is not None) == expect_header
            assert rv.data == b"3"

    is_permanent = True
    app.config["SESSION_REFRESH_EACH_REQUEST"] = True
    run_test(expect_header=True)

    is_permanent = True
    app.config["SESSION_REFRESH_EACH_REQUEST"] = False
    run_test(expect_header=False)

    is_permanent = False
    app.config["SESSION_REFRESH_EACH_REQUEST"] = True
    run_test(expect_header=False)

    is_permanent = False
    app.config["SESSION_REFRESH_EACH_REQUEST"] = False
    run_test(expect_header=False)
```  
+++

\
