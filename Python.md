# Python

## pyevn

Install `pyenv` to manage python versions

### Install dependencies

```
brew install openssl readline sqlite3 xz zlib
```

### Install pyenv

```
curl https://pyenv.run | bash
```

## Troubleshooting

### Error pip install pyodbc: #include <sql.h>

```
brew install unixodbc
export LDFLAGS="-L/opt/homebrew/Cellar/unixodbc/2.3.9_1/lib"
export CPPFLAGS="-I/opt/homebrew/Cellar/unixodbc/2.3.9_1/include"
pip install pyodbc
```

