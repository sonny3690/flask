



# test_request_preprocessing_early_return(app, client)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=5c2f1a891e432aec7f48
```
def test_request_preprocessing_early_return(app, client):
    evts = []

    @app.before_request
    def before_request1():
        evts.append(1)

    @app.before_request
    def before_request2():
        evts.append(2)
        return "hello"

    @app.before_request
    def before_request3():
        evts.append(3)
        return "bye"

    @app.route("/")
    def index():
        evts.append("index")
        return "damnit"

    rv = client.get("/").data.strip()
    assert rv == b"hello"
    assert evts == [1, 2]
```  
+++

\
