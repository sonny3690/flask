



# test_exception_propagation(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=b5d082a8afe4e7f20850
```
def test_exception_propagation(app, client):
    def apprunner(config_key):
        @app.route("/")
        def index():
            1 // 0

        if config_key is not None:
            app.config[config_key] = True
            with pytest.raises(Exception):
                client.get("/")
        else:
            assert client.get("/").status_code == 500

    # we have to run this test in an isolated thread because if the
    # debug flag is set to true and an exception happens the context is
    # not torn down.  This causes other tests that run after this fail
    # when they expect no exception on the stack.
    for config_key in "TESTING", "PROPAGATE_EXCEPTIONS", "DEBUG", None:
        t = Thread(target=apprunner, args=(config_key,))
        t.start()
        t.join()
```  
+++

\
