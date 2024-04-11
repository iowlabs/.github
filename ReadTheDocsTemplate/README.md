# Documentando tu repo con Read The Docs y Sphinx :)

Instrucciones para generar documentación en Read The Docs con Sphinx.

*Cabe mencionar que no es necesario tener Sphinx instalado en local si solo se quieren subir los archivos, pues Read The Docs finalmente lo tiene instalado y los utiliza. Pero en caso de que quieras hacer tu propia carpeta /docs o usar los comandos que son fuertemente recomendados, deberías instalarla*

# Copiar carpeta `/docs`

Clone el repositorio y copie la carpeta `/docs` y el archivo `.readthedocs.yaml` directamente en el repositorio que quiera documentar.

# Instalación:

Ya en local hay que instalar Sphinx con los siguientes comandos en consola:

```
pip install sphinx
```

El siguiente paso es para quienes no quieren copiar la carpeta `/docs` y desean realizar el proceso por su cuenta (no habrá seguimiento de ello en este tutorial)

```
cd /path/to/project
mkdir docs
```

Luego, para definir los archivos iniciales (que al copiar `/docs` ya están incorporados) se corre:

```
cd docs
sphinx-quickstart
```

# Sesión en Read The Docs

A continuación, antes de continuar en local es necesario que te asegures de crear una sesión en [Read The Docs](https://about.readthedocs.com/?ref=readthedocs.com) con tu cuenta de github y siempre asegúrate que la organización y/o individuo que hará la documentación tenga los permisos OAuth activados (en la cuenta de Github, *Settings --> Applications >-- Authorized OAuth Apps*)

Una vez que los permisos estén activados podrás importar el repo a elección que quieras a Read The Docs. Crearás un nombre y te pedirá que tengas un archivo .`radthedocs.yaml` que previamente en el paso de **Copiar carpeta docs** ya hiciste. En ese documento tienes que especificar la versión de Ubuntu que quieres que Read The Docs considere, y muy importante, el path del archivo `config.py` que tiene toda la información para que se pueda compilar apropiadamente el repo en Read The Docs. Si en algún momento cambias la ubicación de ese archivo tendrás que cambiar el path en .`radthedocs.yaml`

Luego, dale click a importar repositorio y Read The Docs intentará compilar tu repo, puede que te arroje error, eso puede ser porque hay algo malo en el repo mismo o en la carpeta `/docs`, si fuera lo primero tendrás que intentar debuggear el error por tu cuenta, si fuera lo segundo continúa con el tutorial y de seguro se arregla.

# Revisar las carpetas de `/docs`

Para comprender mejor se explicarán algunas carpetas y archivos importantes:

`config.py:` Contiene la información de `sphinx` y del formato `html` que se desee.  Si quieres generar los archivos `html` localmente asegúrate de instalar en tu máquina todas las extensiones que se incluyen en `config.py` (haciendo `pip install `de las librerias)

`requeriments.txt` Dado que a pesar de que localmente puedes tener instalado varios paquetes, es necesario especificarle a Read The Docs qué librerías y paquetes son necesarias para tu proceso de documentación. En este documento se precisan ellas.

`index.rst` Es la landing page de Read the docs y en ella a través de los comandos `toctree` se llama a otros módulos `.rst` o carpetas que contengan archivos `.rst`

La estructura que deben seguir tus carpetas para que se compilen adecuadamente es:

```
.readthedocs.yaml
docs:
 |--index.rst
 |--modulos.rst 
 |--config.py
 |--make.bat
 |--requirements.txt
 |--_build
 |--_static
 |--_templates
 |--Carpeta_Imagenes
 |--CarpetaModulo_1 
      |--index.rst
 |--CarpetaModulo_2 
      |--index.rst
 |-- ...
 |--CarpetaModulo_n 
      |--index.rst 
```

Los archivos en los que se escribirá la documentación serán los de tipo "CarpetaModulo" en sus respectivos `index.rst`, en ellas escribirás las secciones que te interese documentar.

El archivo `index.rst` principal que está en `/docs` llama al modulo `modulos.rst` que llama a las carpetas "CarpetaModulo". Puedes crear otros macro modulos (como `modulos.rst`) que sean archivos `.rst` pero eso ya depende de cómo quieras organizarlo.

# Comandos Sphinx para testeo local

Si quieres probar cómo Read The Docs va a ir compilando tu carpeta `/docs` puedes, localmente usando `make.bat`, hacer una generación de los archivos `html` de lo que has construido. De la siguiente forma:

```
cd docs
```

```
.\make.bat html
```

Luego, yendo a la carpeta *_build --> html,* encontrarás los archivos `index.html` y `modulos.html` que podrás abrir en el navegador para testear si las funcionalidades de navegación son las de tu agrado.

Repite este proceso si vas haciendo cambios para chequear cómo se actualizan tus `html`

# Compilar en Read The Docs

Una vez que tengas la configuración deseada, pushea tus cambios al repositorio y en tu sesión de Read The Docs, ya en el repositorio importado vas a la opción de compilar. Cuando esté compilado, haces click a *Ver* *Documentación* y ya debería estar subida tu documentación.

Mucho éxito!
