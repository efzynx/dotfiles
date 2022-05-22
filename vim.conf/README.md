<h1 align="center">VIM CONFIGURATION<br><img src="https://i.ibb.co/F3dgM7J/1022px-Vimlogo-svg.png" width="250px"></h1>

### INSTALLATION ON LINUX
#### Arch based
```bash
> sudo pacman -Syu
> sudo pacman -Sy vim
```
#### Debian based
```bash
> sudo apt update && apt upgrade
> sudo apt install vim -y
```
#### Rpm based
```bash 
> su 
> yum install vim
```

### INSTALLATION ON WINDOWS
#### Installation
<ul>
<li> Download the vim file at the following <a href="https://www.vim.org/download.php">link</a></li>
<li> download the file according to your windows version </li>
<li> then install the .exe file as usual </li>
</ul>

### CONFIGURATION
<ul>
<li> first, you can directly download the .vimrc file above by cloning this repository or using wget </li>

```bash
> wget https://raw.githubusercontent.com/efzynx/dotfiles/main/vim.conf/.vimrc
```
<li> the file uses the vim plug for the plugin installation. so you have to install the vim plug in the following way </li>

```bash
> curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
<il> then, you have to install nodejs so that the <a href="https://github.com/neoclide/coc.nvim">coc.nvim</a> plugin doesn't crash </li>
<li> after that, install <a href="https://git-scm.com/downloads">git</a> and change the terminal font using the font from <a href="https://www.nerdfonts.com/font-downloads">nerdfont</a> to support the existing icons on nerdtree and vim-airline </li>
<li> if everything is installed. please open terminal/cmd then open vim and type :PlugInstall then ENTER. the image below as an example </li>
<img src="https://i.ibb.co/FnYt95y/ss-terminal.png" width="250px">
</ul>