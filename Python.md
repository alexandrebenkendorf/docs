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
# Uninstall pyodbc if installed in the environment
pip uninstall pyodbc

# Install unixodbc via brew
brew install unixodbc

#Set Temporary Environment Variable
export LDFLAGS="-L/opt/homebrew/Cellar/unixodbc/2.3.9_1/lib -liodbc -liodbcinst"
export CPPFLAGS="-I/opt/homebrew/Cellar/unixodbc/2.3.9_1/include"

# Install pyodbc in the environment
pip install pyodbc
```
[Source](https://whodeenie.medium.com/installing-pyodbc-and-unixodbc-for-apple-silicon-8e238ed7f216)

### Error installing Pillow

```
The headers or library files could not be found for jpeg, a required dependency when compiling Pillow from source.
error: legacy-install-failure
```

Solved with 

```
brew install libjpeg libtiff little-cms2 openjpeg webp
brew install freetype harfbuzz fribidi
```

### Error libmagic Mac M1

```
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


### Error - AssertionError: database connection isn't set to UTC

If the psycopg2-binary is 2.9, downgrade it to 2.8
```
pip install psycopg2==2.8.6
# or 
pip install psycopg2-binary==2.8.6
```
[Source](https://stackoverflow.com/a/68025007)


#### Error installing psycopg2 < 2.9 Mac M1

```
export LDFLAGS="-L/opt/homebrew/opt/openssl@1.1/lib -L/opt/homebrew/opt/libpq/lib"
export CPPFLAGS="-I/opt/homebrew/opt/openssl@1.1/include -I/opt/homebrew/opt/libpq/include"
pip install psycopg2-binary==2.8.6
```
[Source](https://stackoverflow.com/a/67166417)


### Error gobject-2.0-0 weasyprint Mac M1

```
brew install pango libffi
sudo mkdir /usr/local/lib/
sudo ln -s /opt/homebrew/opt/glib/lib/libgobject-2.0.0.dylib /usr/local/lib/gobject-2.0
sudo ln -s /opt/homebrew/opt/pango/lib/libpango-1.0.dylib /usr/local/lib/pango-1.0
sudo ln -s /opt/homebrew/opt/harfbuzz/lib/libharfbuzz.dylib /usr/local/lib/harfbuzz
sudo ln -s /opt/homebrew/opt/fontconfig/lib/libfontconfig.1.dylib /usr/local/lib/fontconfig-1
sudo ln -s /opt/homebrew/opt/pango/lib/libpangoft2-1.0.dylib /usr/local/lib/pangoft2-1.0
```
[Source](https://stackoverflow.com/questions/69097224/gobject-2-0-0-not-able-to-load-on-macbook)
