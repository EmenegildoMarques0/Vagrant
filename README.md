# Vagrant
# Guia de Aprendizado

Este repositório é um guia prático para aprender e aplicar os principais conceitos do Vagrant. Ele contém etapas detalhadas para instalação, configuração e uso do Vagrant em ambientes de desenvolvimento virtualizados.

## O que é o Vagrant?

O **Vagrant** é uma ferramenta de automação que facilita a criação e configuração de ambientes virtuais. Ele é amplamente utilizado por desenvolvedores para criar ambientes consistentes de desenvolvimento e replicar ambientes de produção localmente.

---

## Pré-requisitos

Antes de começar, você precisa instalar os seguintes softwares:

1. **VirtualBox** (ou outro provedor de virtualização como VMware, Hyper-V, etc.)
   - [Instalar VirtualBox](https://www.virtualbox.org/wiki/Downloads)
   
2. **Vagrant**
   - [Instalar Vagrant](https://www.vagrantup.com/downloads)

---

## Primeiros Passos com Vagrant

### Verificando a Instalação

Após instalar o Vagrant, abra o terminal e verifique se a instalação foi concluída corretamente:

```bash
vagrant --version
```

### Inicializando um Projeto Vagrant

1. Crie um diretório para o seu projeto Vagrant:
    ```bash
    mkdir meu_primeiro_vagrant
    cd meu_primeiro_vagrant
    ```

2. Inicialize o Vagrant no projeto:
    ```bash
    vagrant init
    ```

3. Isso irá gerar um arquivo chamado `Vagrantfile`, onde serão definidas as configurações da sua máquina virtual.

### Comandos Básicos do Vagrant

- Para iniciar a máquina virtual:
  ```bash
  vagrant up
  ```

- Para acessar a máquina virtual via SSH:
  ```bash
  vagrant ssh
  ```

- Para suspender a máquina:
  ```bash
  vagrant suspend
  ```

- Para desligar a máquina:
  ```bash
  vagrant halt
  ```

- Para destruir a máquina:
  ```bash
  vagrant destroy
  ```

---

## Configurando o Vagrantfile

### Usando uma Box Base

No arquivo `Vagrantfile`, você pode definir qual sistema operacional será usado na máquina virtual. Substitua a linha que contém `config.vm.box = "base"` por uma box específica, como o Ubuntu:

```ruby
config.vm.box = "ubuntu/bionic64"
```

### Atualizando e Iniciando a VM

Após editar o `Vagrantfile`, execute o comando para iniciar a VM:

```bash
vagrant up
```

A VM irá iniciar usando a box especificada (neste caso, Ubuntu 18.04). Para acessar a máquina, utilize o comando:

```bash
vagrant ssh
```

---

## Provisionamento de Software na VM

### Automação com Provisionamento

Você pode automatizar a instalação de pacotes na máquina virtual utilizando o provisionamento. No `Vagrantfile`, adicione um script de shell para instalar o Apache automaticamente:

```ruby
config.vm.provision "shell", inline: <<-SHELL
  sudo apt-get update
  sudo apt-get install -y apache2
SHELL
```

### Executando o Provisionamento

Para provisionar a VM (instalar o Apache, neste caso), execute:

```bash
vagrant provision
```

Ou reinicie a VM para aplicar as mudanças:

```bash
vagrant reload
```

Agora, o Apache estará instalado e rodando na sua VM. Você pode verificar isso acessando a máquina e executando:

```bash
vagrant ssh
sudo systemctl status apache2
```

---

## Compartilhamento de Pastas

### Sincronizando Pastas

O Vagrant permite que você compartilhe pastas entre o sistema host (sua máquina) e a VM. No `Vagrantfile`, adicione a linha:

```ruby
config.vm.synced_folder ".", "/vagrant_data"
```

Isso irá compartilhar o diretório do seu projeto com o diretório `/vagrant_data` dentro da VM.

### Testando o Compartilhamento

1. No host (sua máquina), crie um arquivo dentro do diretório do projeto:
    ```bash
    echo "Olá, Vagrant!" > hello.txt
    ```

2. Acesse a VM e verifique se o arquivo foi sincronizado:
    ```bash
    vagrant ssh
    cat /vagrant_data/hello.txt
    ```

---

## Gerenciamento de VMs com Vagrant

### Comandos Úteis

- **Recarregar a VM** (aplica mudanças no `Vagrantfile`):
    ```bash
    vagrant reload
    ```

- **Suspender a VM** (pausa a máquina sem destruí-la):
    ```bash
    vagrant suspend
    ```

- **Destruir a VM** (remove a máquina virtual e todos os dados):
    ```bash
    vagrant destroy -f
    ```

### Criando Novos Ambientes

Você pode criar novos ambientes trocando a box usada no `Vagrantfile`. Experimente usar uma box diferente, como CentOS:

```ruby
config.vm.box = "centos/7"
```

Depois de editar o `Vagrantfile`, execute:

```bash
vagrant up
```

Isso iniciará uma nova VM com o sistema CentOS 7.

---

## Recursos Adicionais

- [Documentação oficial do Vagrant](https://www.vagrantup.com/docs)
- Explore boxes disponíveis no [Vagrant Cloud](https://app.vagrantup.com/boxes/search)

---

## Conclusão

Este repositório cobre as noções básicas do Vagrant, incluindo a criação de ambientes de desenvolvimento virtualizados, provisionamento de software e sincronização de pastas. Com essas ferramentas, você poderá replicar facilmente ambientes de desenvolvimento e aprender a configurar VMs de maneira automatizada.

---
