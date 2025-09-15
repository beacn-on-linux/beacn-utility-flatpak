# Beacn Utility Flatpak Generation

This repository is primarily a way to test an isolated Flatpak generation, as well as be the base for future flathub
contributions. If it works here, it'll work on flathub.

By Default, this will build the latest `main` revision from the [Beacn Utility](https://github.com/beacn-on-linux/beacn-utility)
repository.

### First time setup
Firstly, install the `flatpak-builder` package for your distribution.

Create a Python Environment to work with, then activate it:
```shell 
python -m venv ~/.python_beacn/
source ~/.python_beacn/bin/activate
```

Perform the First Build
```shell
flatpak-builder --repo=beacn-repo --install-deps-from=flathub --force-clean build-dir io.github.beacn_on_linux.beacn-utility.yml
```

Create a local flatpak remote, and install our built app to it
```shell
flatpak --user remote-add --no-gpg-verify beacn-repo beacn-repo
flatpak install --user beacn-repo io.github.beacn_on_linux.beacn-utility
```

### Future Builds
To update the installed package run the following:
```shell
git pull  # Pull latest changes from this repo
source ~/.python_beacn/bin/activate
flatpak-builder --repo=beacn-repo --install-deps-from=flathub --force-clean build-dir io.github.beacn_on_linux.beacn-utility.yml
flatpak update
```

### Cleaning Up
To remove all flatpak files, run the following:
```shell
rm -rf ~/.python_beacn/
flatpak remote-delete beacn-repo
rm -rf ~/.local/share/flatpak/beacn-repo/
```
