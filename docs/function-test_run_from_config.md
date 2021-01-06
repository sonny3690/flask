



# test_run_from_config(monkeypatch, host, port, server_name, expect_host, expect_port, app)
  
+++section;title=Path;hash=bd125ce807d5f02c78ca

`flask/tests/test_basic.py`
  
+++

\
  
+++section;title=Source Code;hash=46d3522b91abb6bf5651
```
def test_run_from_config(
    monkeypatch, host, port, server_name, expect_host, expect_port, app
):
    def run_simple_mock(hostname, port, *args, **kwargs):
        assert hostname == expect_host
        assert port == expect_port

    monkeypatch.setattr(werkzeug.serving, "run_simple", run_simple_mock)
    app.config["SERVER_NAME"] = server_name
    app.run(host, port)
```  
+++

\
