



# test_werkzeug_passthrough_errors(monkeypatch, debug, use_debugger, use_reloader, propagate_exceptions, app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=32703880d0d5e6a2cddc
```
def test_werkzeug_passthrough_errors(
    monkeypatch, debug, use_debugger, use_reloader, propagate_exceptions, app
):
    rv = {}

    # Mocks werkzeug.serving.run_simple method
    def run_simple_mock(*args, **kwargs):
        rv["passthrough_errors"] = kwargs.get("passthrough_errors")

    monkeypatch.setattr(werkzeug.serving, "run_simple", run_simple_mock)
    app.config["PROPAGATE_EXCEPTIONS"] = propagate_exceptions
    app.run(debug=debug, use_debugger=use_debugger, use_reloader=use_reloader)
```  
+++

\
