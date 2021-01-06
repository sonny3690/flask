



# test_run_defaults(monkeypatch, app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=82141086fa6b67ceecb6
```
def test_run_defaults(monkeypatch, app):
    rv = {}

    # Mocks werkzeug.serving.run_simple method
    def run_simple_mock(*args, **kwargs):
        rv["result"] = "running..."

    monkeypatch.setattr(werkzeug.serving, "run_simple", run_simple_mock)
    app.run()
    assert rv["result"] == "running..."
```  
+++

\
