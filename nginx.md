# Nginx

> Este post é parte do curso de criação de uma API Restful com Node.js, Express, Typescript, TypeORM, Postgres, Redis, Docker, e muito mais.

### Instalação do Nginx como proxy reverso

O Nginx configurado como proxy reverso funcionará capturando toda requisição que chegar de fora para a porta 80 do servidor, redirecionando para a porta 3333, onde o Node.js da nossa aplicação está funcionando. Essa configuração cria uma camada de proteção, para que o Node não fique diretamente exposto.

Instalação do Nginx:

```shell
sudo apt install nginx
```

Liberar no firewall o acesso público para a porta 80 no servidor:

```shell
sudo ufw allow 80
```

Arquivo `/etc/nginx/sites-available/apivendas`:

```shell
server {
  listen 80 default_server;
  listen [::]:80 default_server;
	server_name apivendas.aluiziodeveloper.cf;

	location / {
		proxy_pass http://localhost:3333;
		proxy_http_version 1.1;
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection 'upgrade';
		proxy_set_header Host $host;
		proxy_cache_bypass $http_upgrade;
	}
}
```

> Para servir mais de uma aplicação dessa forma através do Nginx, basta criar outros arquivos como o que criamos, alterando o "server_name" e a porta interna em que a aplicação funcionará.

Habilitar a configuração no Nginx:

```shell
sudo ln -s /etc/nginx/sites-available/apivendas /etc/nginx/sites-enabled
```

Verificar a sintaxe do arquivo de configuração:

```shell
sudo nginx -t
```

Reiniciar o Nginx:

```shell
sudo service nginx restart
```


