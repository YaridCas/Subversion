## Subversion ##


### Introducción ###

Subversion es un sistema centralizado de control de versiones. En otras palabras, es un sistema que permite llevar el control de los cambios realizados por una o más personas a una serie de documentos a través del tiempo.

En un proyecto podemos tener muchos documentos de diversos tipos, como *HTML* o código de *Phyton*. Los documentos pueden estar cambiando constantemente y ser modificados por diversas personas. En el ciclo de trabajo diario, esta situación puede ocasionar cambios perdidos y severos problemas de coordinación, lo que degenera en tiempo perdido y baja de productividad para todos los miembros del equipo de desarrollo.

Un sistema de control de versiones se encarga de llevar el control de todas estas modificaciones a los documentos del proyecto. Un desarrollador solamente tiene que encargarse de guardar sus cambios al proyecto y el sistema se ocupa de integrarlos con los cambios de los otros miembros del equipo y de asegurarse de que no existan conflictos.

Adicionalmente, utilizar un sistema de control de versiones nos permite cosas como comparar la más reciente versión de un documento con versiones anteriores, identificar quien ha realizado cuales cambios en el código y designar un conjunto de documentos específicos como una 'entrega' del proyecto que queda identificada con las versiones de cada uno de los documentos en el instante de la definición.   

### Comandos básicos de Subversion ###

Una vez que se tiene un proyecto o estructura en el repositorio, la manera de trabajar con Subversion es extraer una copia del proyecto para realizar cambios y subirlos al terminar. Esta copia del proyecto se conoce como *copia de trabajo* y Subversion puede determinar exactamente que documentos se han agregado o han sido modificados mientras trabajas en ello. 

### *checkout* - Crear una copia de trabajo ###

El proceso de obtener del repositorio una copia del proyecto se conoce como **svn checkout**. El parámetro que se pasa al comando además del path en el repositorio que queremos copiar es el nombre de la carpeta donde colocaremos la copia:

`$ svn co svn://localhost/opt/svn/proyecto_ejemplo proyecto_ejemplo`  
`A    proyecto_ejemplo/trunk`  
`A    proyecto_ejemplo/tags`  
`A    proyecto_ejemplo/branches`  
`Checked out revision 2`

### *info* - Obtener información básica del repositorio ###

Al cambiarnos dentro del directorio de la copia de trabajo, Subversion puede reconocer que estamos utilizando un repositorio. En cualquier momento podemos obtener los datos del repositorio donde estamos conectados utilizando el comando **svn info**:

`$ cd proyecto_ejemplo`  
`$ svn info`  
`Path: .`  
`URL: svn://localhost/opt/svn/proyecto_ejemplo`  
`Repository Root: svn://localhost/opt/svn`  
`Repository UUID: 073e038a-3ebf-4a60-b88a-b0abaccd7367`  
`Revision: 2`  
`Node Kind: directory`  
`Schedule: normal`  
`Last Changed Author: juan`  
`Last Changed Rev: 2`  
`Last Changed Date: 2010-04-09 00:30:57 -0500 (Fri, 09 Apr 2010)`  

El comando **svn info** nos devuelve entre otras cosas el URL de donde se extrajo el directorio donde estamos trabajando (URL), el URL de la raíz del repositorio (*Repository Root*), la revision o versión al momento del checkout (*Revision*), el autor del ultimo cambio (*Last Changed Author*) y la fecha de ese cambio (*Last Changed Date*).


###*status* - Conocer el estado de nuestras modificaciones###

Una vez que comenzamos a hacer modificaciones dentro del directorio del proyecto, Subversion lleva la cuenta de los cambios que hemos realizado y en cualquier momento podemos consultarlos:

`$ cd trunk`  
`$ echo "La capital de Francia es Tokio" > info.txt`  
`$ svn status`  
`?      info.txt`  

En el ejemplo anterior, creamos un archivo de texto con una sola linea, llamado *info.txt*. Una vez creado el archivo, utilizamos el comando **svn status** para mostrar como Subversion ha detectado que existe un nuevo archivo en el directorio. El signo de interrogación que aparece antes del nombre, significa que el archivo en cuestión no esta bajo control de versiones y Subversion lo desconoce.

###*add* - Agregar documentos al proyecto###

Para agregar ese archivo al proyecto, utilizamos el comando **svn add**:

`$ svn add info.txt`  
`A      info.txt`  

Subversion agrega el archivo *info.txt* a los que se encuentran bajo control de versiones, por lo que el status muestra ahora la letra *A* junto al nombre. Es importante hacer notar que este comando únicamente tiene efecto en nuestra copia de trabajo y no sube de inmediato el archivo al repositorio.

El comando **svn add** no esta limitado a agregar un solo archivo, por supuesto. Es posible incluir como parámetro cualquier cantidad de archivos. Si se agrega un directorio, todos los archivos contenidos en el serán agregados recursivamente al proyecto.

###*commit* - Como guardar nuestros cambios en el repositorio###

Podemos hacer todos los cambios que necesitemos en nuestra copia de trabajo, si bien se recomienda subir la información al menos al final de cada sesión de trabajo y de preferencia cada vez que terminemos una tarea especifica de edición. La razón es que mientras mas tiempo pasemos sin subir los cambios, mas difícil puede resultar integrarlos con otros cambios al repositorio, especialmente si muchas personas tienen acceso al mismo.

A la operación de subir los cambios al repositorio se le llama commit. Una vez que hemos terminado nuestra sesión de trabajo, utilizamos ese comando para guardarlos en el repositorio:

`$ svn commit -m 'se agrego archivo info'`  
`Adding         trunk/info.txt`  
`Transmitting file data .`  
`Committed revision 3.`  

El comando **svn commit** guarda todos los cambios realizados desde que inicio la sesión. En caso de no querer guardar todo, es posible especificar los archivos que deben subirse.