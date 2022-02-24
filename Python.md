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

## Error libmagic Mac M1

````
raise ImportError('failed to find libmagic.  Check your installation')
ImportError: failed to find libmagic.  Check your installation
```

Uninstall `python-magic` and `libmagic`
Install via `brew`

```
brew install libmagic
```
[Source](https://blog.balasundar.com/install-older-versions-of-python-using-miniconda-on-mac-m1)
> The `sudo env ARCHFLAGS...` didn't work for me

then 

```
sudo gem install ruby-filemagic -v 0.7.2 -- \
  --with-magic-lib=$(brew --prefix)/lib \
  --with-magic-include=$(brew --prefix)/include
```
[Source](https://stackoverflow.com/a/71077610)

then reinstall `python-magic`
