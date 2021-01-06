



# test_run_server_port(monkeypatch, app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=a054f4a69cf15cb1c249
```
def test_run_server_port(monkeypatch, app):
    rv = {}

    # Mocks werkzeug.serving.run_simple method
    def run_simple_mock(hostname, port, application, *args, **kwargs):
        rv["result"] = f"running on {hostname}:{port} ..."

    monkeypatch.setattr(werkzeug.serving, "run_simple", run_simple_mock)
    hostname, port = "localhost", 8000
    app.run(hostname, port, debug=True)
    assert rv["result"] == f"running on {hostname}:{port} ..."
```  
+++

\
