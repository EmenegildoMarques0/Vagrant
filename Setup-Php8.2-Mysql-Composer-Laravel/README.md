
---

# Ambiente de Desenvolvimento com Vagrant: PHP 8.2, MySQL e Laravel

Este projeto utiliza **Vagrant** para provisionar um ambiente de desenvolvimento com **PHP 8.2**, **MySQL** e **Laravel**. Ele é ideal para quem deseja um ambiente replicável, configurado automaticamente, e que pode ser usado para desenvolvimento de aplicações Laravel.

## Pré-requisitos

- [Vagrant](https://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/)

## Configuração do Ambiente

### Passo 1: Inicializar a VM

No diretório do seu projeto, rode o seguinte comando para inicializar a máquina virtual e aplicar o provisionamento:

```bash
vagrant up
```

### Passo 2: Acessar a VM

Após a VM estar rodando, acesse-a via SSH com o comando:

```bash
vagrant ssh
```

### Passo 3: Navegar até o projeto Laravel e rodar o servidor

Dentro da máquina virtual, navegue até o diretório do projeto Laravel e inicie o servidor Laravel:

```bash
cd /vagrant/laravel-app
php artisan serve --host=0.0.0.0 --port=8000
```

### Acessando a aplicação Laravel

Agora, sua aplicação Laravel estará disponível em:

```
http://localhost:8000
```

Abra o navegador e acesse esse endereço na máquina host.

## Detalhes do Ambiente Provisionado

O provisionamento automático irá instalar e configurar o seguinte ambiente:

- **PHP 8.2** com as extensões necessárias para o Laravel (mbstring, xml, bcmath, zip, mysql, curl).
- **MySQL** configurado com um banco de dados `laravel_db`.
- **Composer** instalado globalmente.
- Um projeto Laravel criado automaticamente no diretório `/vagrant/laravel-app` (opcionalmente, você pode modificar o nome do projeto ou importar um existente).

## Comandos Úteis

- Para parar a VM:

  ```bash
  vagrant halt
  ```

- Para reiniciar a VM:

  ```bash
  vagrant reload
  ```

- Para reprovisionar a VM (aplicar novamente o script de provisionamento):

  ```bash
  vagrant provision
  ```



