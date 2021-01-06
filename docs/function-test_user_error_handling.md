



# test_user_error_handling(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=d357eb524ebfd41fb761
```
def test_user_error_handling(app, client):
    class MyException(Exception):
        pass

    @app.errorhandler(MyException)
    def handle_my_exception(e):
        assert isinstance(e, MyException)
        return "42"

    @app.route("/")
    def index():
        raise MyException()

    assert client.get("/").data == b"42"
```  
+++

\
