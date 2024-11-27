# Instalando um linux no WSL

Primeiro verificamos pello Powershell se temos uma instalação do Ubuntu instalaado no WSL

```powershell
PS> wsl --list
```

Se não tiver a versão que vc deseja, instale com o comando

```powershell
PS> wsl --install -d Ubuntu-24.04
```

ou de uninstall com o comando

```powershell
PS> wsl --unregister Ubuntu-24.04
```

# Configurando o shell

Instale o `oh-my-posh` com o comando

```shell
$ curl -s https://ohmyposh.dev/install.sh | bash -s
```
Após isso baixe o tema desejado (`quick-term.omp.json`), coloque em um folder (`oh-my-posh-themes`) e acrescente no final do arquivo `.profile` o seguinte comando

```txt
eval "$(oh-my-posh init bash --config ~/oh-my-posh-themes/quick-term.omp.json)"
```

Saia do console e entre novamente

# Configurando o Git

O `git` já vem instalado, sendo necessário setar o seu usuário

```shell
$ git config --global user.name "Marcio Cruz de Almeida"
$ git config --global user.email "marciocadev@gmail.com"
$ ssh-keygen -t ed25519 -C "marciocadev@gmail.com"
$ cat ~/.ssh/id_ed25519.pub
```

Copie a chave exibida para o Github

# Instalando o Docker

Para instalar o docker no Ubuntu temos de executar alguns comandos conforme o website oficial do  [Docker Engine](https://docs.docker.com/engine/install/ubuntu/)

```shell
$ sudo apt-get update

$ sudo apt-get install ca-certificates curl

$ sudo install -m 0755 -d /etc/apt/keyrings

$ sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

$ sudo chmod a+r /etc/apt/keyrings/docker.asc

$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

$ sudo apt-get update
```

Instalando a última versão do docker

```shell
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Uma vez instalada para não seja necessário utilizar `sudo` a cada comando precisamos criar um grupo para usar o docker a atribuir nosso usuário a este grupo

```shell
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
```

Agora simplesmente feche o console e abra novamente e seu usuário terá permissão para utilizar o docker sem o comando `sudo`

# Client AWS
Instale o `aws-cli`

```shell
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

$ unzip awscliv2.zip
$ sudo ./aws/install
$ rm -rf awscliv2.zip
```

Crie o folder `~/.aws` e os arquivos `config` e `credentials` dentro dele

no arquivo `config` coloque o seguinte conteudo
```txt
[default]
region=us-east-1
output=json
```

no arquivo `credentials` coloque os dados da sua credencial conforme abaixo

```txt
[default]
aws_access_key_id=???
aws_secret_access_key=???
```

# Client Terraform

Execute os commando abaixo
```shell
$ sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

$ wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

$ gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint

$ echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

$ sudo apt update && sudo apt-get install terraform
```

# Linguagens

O `Ubuntu 24.04` já vem instalado com o `python 3.12.3`

É necessário instalar o `node`

## Instalando o Node

Para instalar o `node v22.11.0` e `npm 10.9.0`, instale o `nvm` conforme abaixo

```shell
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
```

Agora simplesmente feche o console, abra novamente e execute o comando

```shell
$ nvm install 22
```

Verificando as versões

```shell
$ node -v
v22.11.0

$ npm -v
10.9.0
```

Caso necessite do Volta execute o comando e configure a versão padrão no node
```shell
$ curl https://get.volta.sh | bash

$ volta install node@22.11.0

$ volta -v
2.0.1
```

## Instalando o Rust

Para instalar o `rust` execute o commando abaixo
```shell
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
Para verificar a versão
```shell
$ rustc --version
rustc 1.82.0 (f6e511eec 2024-10-15)
```
