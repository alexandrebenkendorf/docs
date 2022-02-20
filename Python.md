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

Add to `~/.zprofile`

```
alias python='python3'

export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

> To see list of availables use `pyenv install --list`
> To filter the list from 3.6 through 3.8 use `pyenv install --list | grep " 3\.[678]`


## Troubleshooting


If you need to have bzip2 first in your PATH, run:

```
echo 'export PATH="/opt/homebrew/opt/bzip2/bin:$PATH"' >> ~/.zshrc
```

For compilers to find bzip2 you may need to set, in `~/.zshrc`:

```
export LDFLAGS="-L/opt/homebrew/opt/bzip2/lib"
export CPPFLAGS="-I/opt/homebrew/opt/bzip2/include"
```

Not sure if this works:

```
export LDFLAGS="-L/usr/local/opt/zlib/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include"
```


### configure: error: Unexpected output of 'arch' on OSX
``` 
arch -x86_64 pyenv install 3.7.5
```
