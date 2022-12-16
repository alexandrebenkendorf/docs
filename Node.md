# Node

## Installation

```
brew install node
```

## NVM - Node Version Manager

[Documentation](https://github.com/nvm-sh/nvm)

## Installation

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

Add to `~/.zprofile`:

```
# NVM
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm

# Autoload NVM
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```

## Usage

To download, compile, and install the latest release of node, do this:

```
nvm install node # "node" is an alias for the latest version
```

To install a specific version of node:

```
nvm install 14.7.0 # or 16.3.0, 12.22.1, etc
```

The first version installed becomes the default. New shells will start with the default version of node (e.g., nvm alias default).

You can list available versions using `ls-remote`:

```
nvm ls-remote
```

And then in any new shell just use the installed version:

```
nvm use node
```

### Automatic change

Create `.nvmrc` file on root folder of your app to allow automatically node version change using.

Open the terminal on your root app folder

#### Using current node version

Run

```
node -v > .nvmrc
```

#### Create a file manually

Create a `.nvmrc` file with the version you want i.g.:

```
v12.22.8
```

## Troubleshoot

### Error installing under v15

For anything under v15, you will need to install node using Rosetta 2. 
[Solution here](https://github.com/nvm-sh/nvm/issues/2350#issuecomment-734132550)


Or enable it on iTerm2:

![image](https://user-images.githubusercontent.com/11325962/208135760-b4fff8e5-2f6f-4c07-aaf8-242565ca888d.png)
![image](https://user-images.githubusercontent.com/11325962/208136396-b637753c-1f7c-4bf9-a239-a97ae47249f4.png)

[Source](https://github.com/nvm-sh/nvm/issues/2350#issuecomment-740379270)
