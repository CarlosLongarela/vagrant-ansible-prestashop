# VAP (Vagrant Ansible PrestaShop)

VAP: Proyecto para el desarrollo de módulos y temas de PrestaShop 1.7.1 con un entorno Ubuntu Xenial y Nginx, MariaDB y PHP 7.1 realizando el aprovisionamiento desde Ansible en la máquina virtual Vagrant (con VirtualBox).

## Tabla de Contenidos

- [Resumen](#resumen)
  - [PrestaShop](#prestashop)
  - [Vagrant](#vagrant)
  - [Ansible](#ansible)
  - [ngrok](#ngrok)
- [Instalación](#instalación)
- [Uso Básico](#uso-básico)
  - [Back Office](#back-office)
  - [MySQL](#mysql)
  - [PHPmyAdmin](#phpmyadmin)
  - [XDebug](#xdebug)
  - [Vagrant](#vagrant)
- [Desarrollo](#development)
  - [Módulos](#module)
  - [Temas](#theme)
  - [Acceder a servidor local](#acceder-a-servidor-local)

## Resumen

### PrestaShop

PrestaShop is a free and Open Source e-commerce web application, committed to
providing the best shopping cart experience for both merchants and customers.
It is written in PHP, is highly customizable, supports all the major payment
services, is translated in many languages and localized for many countries,
has a fully responsive design (both front and back office), etc.

The development environment includes PrestaShop version 1.7.1

### Vagrant

[Vagrant](https://www.vagrantup.com/) provides easy to configure,
reproducible, and portable work environments built on top of
industry-standard technology and controlled by a single consistent
workflow to help maximize the productivity and flexibility of
you and your team.

To achieve its magic, Vagrant stands on the shoulders of giants. Machines
are provisioned on top of VirtualBox, VMware, AWS, or any other provider.
Then, industry-standard provisioning tools such as shell scripts, Chef, or
Puppet, can be used to automatically install and configure software on
the machine.

La máquina virtual está basada en Ubuntu 16.04 LTS (Xenial Xerus).

### Ansible

[Ansible](https://www.ansible.com/), es una herramienta de aprovisionamiento para sistemas Linux, Unix, y Window, que realiza tareas administrativas como instalar paquetes, configurar servicios, añadir bases de datos y usuarios, etc. desde un terminal y sin instalar nada en el servidor (sólo requiere acceso por SSH).

No es necesario tener instalado Ansible ne nuestro sistema ya que se ejecuta desde la propia virtual al utilizar `ansible_local`.

### ngrok

[ngrok](https://ngrok.com/) is a handy tool and service that allows you
tunnel requests from the wide open Internet to your local machine when
it's behind a NAT or firewall. This is useful in a number of cases,
such as when you want to show your client the current development status,
but you haven't yet deployed your code to an Internet accessible
host or PaaS.

## Instalación

Primero, tenemos que asegurarnos que tenemos [VirtualBox](https://www.virtualbox.org/wiki/Downloads) y
[Vagrant](https://www.vagrantup.com/downloads.html) instalados.

Después abrimos el terminal y `cd` en el directorio que contiene este README:

```shell
$ cd RUTA-AL-PROYECTO
```

Ahora sólo necesitamos levantar Vagrant y se instalará y configurará todo:

```shell
$ vagrant up
```

## Uso Básico

### Panel de contro PrestaShop

Se puede acceder al panel de control del PrestaShop en la siguiente url:

- [prestashop.test/admin123](http://prestashop.test/adminvap72)

Para autenticarse en el panel de control utilizaremos las siguientes credenciales:

- Usuario: vap@prestashop.test
- Clave: prestashop

### MariaDB

Se puede acceder a la base de datos MariaDB con las siguientes credenciales:

- Host: localhost
- Puerto: 3366
- DB: prestashop
- Usuario: prestashop
- Clave: prestashop

### PHPmyAdmin

Se puede acceder al PHPmyAdmin desde la siguiente url:

- [prestashop.test/phpmyadmin](http://prestashop.test/phpmyadmin)
- Usuario: prestashop
- Contraseña: prestashop

### XDebug

XDebug is included and enabled by default.

Para configurar XDebug necesitamos:

- set the server source root to `/var/www/`
- set the local source root to your current workspace

Ahora nos conectamos a XDebug en el puerto 9000

Nota: Las configuraciones de XDebug se pueden configurar en el php.ini del rol _CarlosLongarela.php7_.

### Vagrant

Vagrant está [muy bien documentada](https://www.vagrantup.com/docs/) pero aquí están algunos comandos:

- `vagrant up` - inicia la máquina virtual y la aprovisiona
- `vagrant suspend` - pone la máquina virtual _a dormir_ y con `vagrant resume` la devolvemos a su estado anterior
- `vagrant halt` - realiza un apagado ordenado de la máquina virtual
- `vagrant reload` - realiza un reinicio de la máquina virtual
- `vagrant ssh` - se conecta a la máquina virtual por ssh

Usuario ssh: ubuntu

## Desarrollo


Para el desarrollo tanto de módulos como de temas de PrestaShop, tenemos compartido el directorio raíz de la web de PrestaShop, por lo que podemos editar con nuestras herramientas favoritas de desarrollo desde `./www/public` en nuestra máquina local.

- **Temas** en `./www/public/themes`
- **Módulos** en `./www/public/modules`

### Acceder a servidor local

Don’t constantly redeploy your in-progress work to get feedback from clients.
ngrok creates a secure public URL (https://yourapp.ngrok.io) to a local webserver
on your machine. Iterate quickly with immediate feedback without interrupting
flow.

To expose your local server you need to do the following steps:

```
$ vagrant ssh
$ cd /var/www
$ ./ngrok http 80
```

Now you only need to copy the public URL and send it to your client.

CAUTION: You need to change the PrestaShop Site URL to the public ngrok URL.
Otherwise PrestaShop will redirect you to localhost.
