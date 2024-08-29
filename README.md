# Helix Configuration for Rust on Fedora 40
It took a bit of time to search for all the things and understand how to setup helix text editor, what they do. This repository collects my findings on installing and setting up helix text editor for rust language and fedora workstation 40. So, I have a old laptop so need a lightweight IDE for development and helix along with it's lsp is a powerful and lighweight(well rust-analyzer is not but still consumes less ram).

## Helix Installation
I am using fedora workstation 40, however helix is available for all of the OS and distros. Fortunately, it's available to be installed using package manager as well. Refer to the [installtion guide according to os/distro](https://docs.helix-editor.com/package-managers.html)
1. **Install Helix using Package Manager**
```bash
sudo dnf install helix -y
```  
This installs the helix text editor on your system, you can launch helix using the following command from terminal, or this is available to be launched using app.
```bash
hx
hx filename/directory
```
If you use just hx, then you can use the `:open filename` to open that file. This should be visible on the bottom left. 
