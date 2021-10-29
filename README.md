# OpenBubi-Docs
Documentation for the OpenBubi software

## Deploying locally

To deploy this documentation locally,

1. Clone this repository

```bash
git clone https://github.com/PiciAkk/OpenBubi-Docs
```

2. Go to the newly cloned folder

```bash
cd OpenBubi-Docs
```

3. Install all the dependencies

```bash
pip install -r requirements.txt
```

4. Start the webserver

```bash
mkdocs serve -a 0.0.0.0:8080
```

or

```bash
make
```

## Directory structure

Markdown files: `docs/`

Mkdocs config file: `mkdocs.yml`

Makefile: `Makefile`

Requirements
