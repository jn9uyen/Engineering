# UV

[UV](https://docs.astral.sh/uv/) is an extremely fast Python package and project manager, written in Rust.

To create virtual environments (`venv`) using UV, go instead a project and create the `venv`. UV will create the `venv` folder directly inside the project directory.
```
uv venv <name>
```
e.g.
```
uv venv ai_fb_creatives
```

Then activate the venv:
```
source ai_fb_creatives/bin/activate
```

Then install python packages:
```
uv pip install pandas
```

If an error message appears due to an SSL/TLS certificate verification failure:
```
× Failed to fetch: `https://pypi.org/simple/pip/`

  ├─▶ Request failed after 3 retries

  ├─▶ error sending request for url (https://pypi.org/simple/pip/)

  ├─▶ client error (Connect)

  ╰─▶ invalid peer certificate: UnknownIssuer

  help: Consider enabling use of system TLS certificates with the `--native-tls` command-line flag
```

the fix is to use the `--native-tls` flag with your uv command, just as the error message suggests; e.g.
```
uv pip install --upgrade pip --native-tls
```

To make the change permanent:
```
export UV_NATIVE_TLS=1

echo 'export UV_NATIVE_TLS=1' >> ~/.zshrc
source ~/.zshrc
```
