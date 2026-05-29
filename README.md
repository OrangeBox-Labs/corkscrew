# Bienvenido a Corkscrew
======================

**NOTA:** Este es fork es para preservar el proyecto original, es una herramienta que usamos en OrangeBox como pentest para labs de seguridad. 

## Introducción

Corkscrew es una herramienta para tunelizar SSH a través de proxies HTTP, pero... puedes
encontrarle otros usos.

Corkscrew ha sido compilado en:

- HPUX
- Solaris
- FreeBSD
- OpenBSD
- Linux
- Win32 (con Cygwin)

Corkscrew ha sido probado con los siguientes proxies HTTP:

- Gauntlet
- CacheFlow
- JunkBuster
- Apache mod_proxy

Por favor abre un pull request si logras hacerlo funcionar en otros proxies o compilarlo
en otras plataformas.


## ¿Dónde lo consigo?

El sitio principal de distribución de Corkscrew era
[agroman.net/corkscrew](https://web.archive.org/web/20170510154150/http://agroman.net/corkscrew/),
sin embargo el sitio parece haber caído y este repositorio existe para mantener
el código disponible. La nueva ubicación es entonces
[github.com/bryanpkc/corkscrew](https://github.com/bryanpkc/corkscrew).


## ¿Cómo lo instalo?

Primero necesitas instalar herramientas de desarrollo:

```bash
# Para distribuciones basadas en Debian (Ubuntu, ElementaryOS, ...)
sudo apt install build-essential

# Para distribuciones basadas en Red Hat (CentOS, Fedora, ...)
sudo yum groupinstall 'Development tools'
```

Debes clonar el repositorio y luego entrar al directorio fuente de `corkscrew`
y ejecutar:

```bash
autoreconf --install
./configure
make
sudo make install
```

Esto compilará `corkscrew` y lo copiará en `/usr/local/bin/corkscrew`.

Si quieres profundizar en la configuración, revisa el archivo [INSTALL](./INSTALL)
que contiene información general sobre el sistema de compilación.


## ¿Cómo se usa?

Configurar Corkscrew con SSH/OpenSSH es muy simple. Agregar la siguiente línea
a tu archivo `~/.ssh/config` normalmente es suficiente (reemplaza
`proxy.example.com` y `8080` con los valores correctos):

```text
ProxyCommand /usr/local/bin/corkscrew proxy.example.com 8080 %h %p
```

**NOTA**: La sintaxis de la línea de comandos cambió desde la versión 1.5.
Ten en cuenta que el puerto del proxy YA NO es opcional y es obligatorio en la línea de comando.


## ¿Cómo uso la autenticación HTTP?

Necesitarás crear un archivo que contenga tu usuario y contraseña en el formato:

```text
username:password
```

Se recomienda guardar este archivo en tu directorio `~/.ssh`.

Después de crearlo debes asegurarte de que los permisos sean correctos para que nadie
pueda leerlo:

```text
chmod 600 myauth
```

Ahora debes modificar la línea `ProxyCommand` en tu archivo `~/.ssh/config`.
Ejemplo:

```text
ProxyCommand /usr/local/bin/corkscrew proxy.work.com 80 %h %p ~/.ssh/myauth
```

La funcionalidad de autenticación HTTP es muy nueva y no ha sido probada
extensamente, por lo que el comportamiento puede variar. Si encuentras problemas
al usarla, por favor envía un correo. Sería útil incluir:

- Versión del proxy (ej: Gauntlet Proxy, Microsoft Proxy Server, etc)
- Sistema operativo donde estás ejecutando corkscrew
- Sintaxis del comando que estás usando
- Cualquier mensaje de error visible

**NOTA**: Se han reportado problemas con la autenticación en Microsoft Proxy Server.
Los problemas son intermitentes y probablemente relacionados con configuraciones
de balanceo de carga. El comportamiento puede variar.


## ¿Quién contribuyó?

El autor principal es Pat Padgett. Pero la información de contacto ya no funciona,
así que solo queda el nombre.

Bryan Chan creó este repositorio y ajustó ligeramente el código. Luego
Rémy Sanchez mejoró la documentación.
