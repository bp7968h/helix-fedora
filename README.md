# Helix Configuration for Rust on Fedora 40
So, I have a old laptop so need a lightweight IDE for development and helix along with it's lsp is a powerful and lighweight(well rust-analyzer is not but still consumes less ram). It took a bit of time to setup helix for rust on fedora (linux) and understand the what and how. This repository collects my findings on installing and setting up helix text editor for rust language and fedora workstation 40. 

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
If you use just `hx`, then you can use the `:open filename` to open that file. This should be visible on the bottom left. The bottom view with all information such as filename, mode, file-type is called *status line*.

2. **Edit Helix Look and Feel**

If you want to change the look and feel of the helix editor, you now need to add configuration file. When you opened helix for the first time, it initializes `.config` directory on your home directory `~/.`
  - Create helix config file.
```bash
cd ~/.config
hx config.toml
```
  - Add required look and feel.

Simply, this config file is used to configure the helix editor, like themes, line numbers, what should appear where etc. For this you can refer to the [`config.toml`](https://github.com/bp7968h/helix-rust-fedora/main/config.toml) given in this repository which can be used as a building block, and you can find more [about each field in this documentation](https://docs.helix-editor.com/configuration.html) 

>Now, as Helix editor is working in desired state, now we can configure helix to make our life easier while working with Rust. To check the health and configuration of Rust language support  we can use the following command: In fact, you can use any other language here `hx --health` for all the languages.
```bash
hx --health rust
```
## Rust Installation
If you haven't installed rust then you can install rust following the below process, if you have already got rust then, you also need some toolchain such as:
  * `rust-analyzer` : Language server for rust, provides feature like code completion, goto definition, and inline documentation.
  * `clippy` : Clippy is a linter for Rust that helps catch common mistakes and improve code quality.
  * `rustfmt` : Rustfmt automatically formats your Rust code according to style guidelines.
1. **Install Rust using Script**
```bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```
After installation you can install additional tools like rust-analyzer, clippy, rustfmt, cargo. These might be already installed with the above script, check using:
```bash
rustup component list | grep installed
```
If rust-analyzer (language server), clippy (linter), rustfmt (format code) is not installed then install using the below command:
```bash
rustup component add rust-analyzer clippy rustfmt
```

2. **Setup Helix for Rust**

Now, that you have rust and helix, it's time to configure helix with rust language server, linting and format capabilities. For this, we need `languages.toml` in the `.config` directory.
  - Create language config file
```bash
cd ~/.config
hx languages.toml
```
  - Add required configuration to the files

This configuration contains settings for language servers and language-specific settings. For this you can refer to the [`languages.toml`](https://github.com/bp7968h/helix-rust-fedora/main/languages.toml) given in this repository which can be used as a building block, and you can find more [about each field in this documentation](https://docs.helix-editor.com/languages.html). Also some of the settings come from rust-analyzer, [check it out here](https://rust-analyzer.github.io/manual.html).
  - Add debugging capabalities

Now you also need debugging capabilities, for this you need to add `lldb-dap` which is the default debug adapter protocol for rust in helix. Use the below command which installs lldb with this comes lldb-dap.
```bash
sudo dnf install lldb
```

Now when you look into the health of rust using `hx --health rust`, everything should be in place as shown below:
```bash
hx --health rust
```

You are all set to work on your next big project using helix and rust. 
Happy coding!
