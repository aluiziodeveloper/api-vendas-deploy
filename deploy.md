# Build na Digital Ocean

> Este post é parte do curso de criação de uma API Restful com Node.js, Express, Typescript, TypeORM, Postgres, Redis, Docker, e muito mais.

> [Página de Documentação da Digital Ocean](https://www.digitalocean.com/docs/droplets/how-to/create/).

## Primeiro Acesso ao Servidor

- Acessar com: `ssh root@<ip-do-servidor>`.

- Criar um usuário:

`adduser deploy`

- Incluir o usuário deploy no grupo "sudo":
 
`usermod -aG sudo deploy`

- Criar a pasta ".ssh" do usuário deploy:

`mkdir -p /home/deploy/.ssh`

- Copiar o arquivo de autorização para autenticação para a pasta do usuário deploy:

`cp ~/.ssh/authorized_keys /home/deploy/.ssh/`

- Alterar o proprietário dos arquivos na pasta home do usuário deploy, para que o próprio seja o dono:

`chown -R deploy:deploy /home/deploy/.ssh/`

- Atualizar o `apt`:

`apt update`

- Após a atualização dos pacotes pode surgir uma tela de configuração de pacote, pedindo para escolher uma opção. Selecione a opção `keep the local version currently installed` para todas as solicitações.

Instalar o node.js:

```shell
curl -sL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```

```shell
apt install -y nodejs
```

Instalar o Yarn:

Acessar o site do Yarn com a [versão 1.22.x](https://classic.yarnpkg.com/en/docs/), Get Started e Instalation:

```shell
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -

echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

sudo apt update

sudo apt install -y yarn
```

