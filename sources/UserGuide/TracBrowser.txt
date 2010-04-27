.. _TracBrowser:

Visor del repositorio
*********************

El visor del repositorio que ofrece Trac puede ser usado para
explorar directorios y revisiones específicas de ficheros
almacenados en el repositorio del sistema de control de
versiones configurado.

Las entradas de los directorios son mostradas en listas con columnas
ordenables. Las listas pueden ser ordenadas por *nombre*, *tamaño* o
*fecha* haciendo clic en la cabecera de la columna. El orden puede ser
invertido al hacer clic de nuevo en la cabecera de la columna
correspondiente.

El visor puede ser usado para navegar a través de la estructura de 
directorios al hacer clic sobre ellos. Haciendo clic sobre un nombre
de fichero mostrará el contenido del mismo. Haciendo clic en el número
de revisión de un fichero o directorio le mostrará el historial de revisiones
de Trac para ese directorio o fichero. Note que también existe un enlace
de *historial de revisiones* que hará lo mismo para la ruta que está
siendo examinada actualmente.

También es posible visualizar los directorios o ficheros tal como eran
en su historia, en cualquier revisión del repositorio. El comportamiento
por omisión es mostrar la última revisión, pero puede elegir cualquier otro
número de revisión al usar el campo de entrada *Ver Revisión* que se
encuentra en el tope de la página.

Desde la versión 0.11 de Trac, en el tope de la página, existe un menú
desplegable que puede usar para seleccionar algunas ubicaciones interesantes
en el repositorio, por ejemplo las ramas (*branches*) o etiquetas (*tags*). 
Para *subversion*, esta lista contiene por omisión algunas ramas (``trunk``
y cualquier sub-directorio que se encuentre en el nivel superior de la última
revisión de los ``branches``) y algunas etiquetas (cualquier sub-directorio
que se encuentre en el nivel superior de la última revisión de ``tags``).
Esta lista puede ser configurada para casos más avanzados.

Si su navegador tiene la opción de Javascript activado, usted podrá extender o 
contraer directorios en sitio al hacer clic en la flecha que se encuentra al lado
izquierdo de los directorios. Alternativamente, el teclado también puede ser usado
para esto: utilice ``j`` y ``k`` para ir a la entrada siguiente o previa, y ``o``
( o ``Enter``) para expander o contraer el estado del directorio seleccionado
o visitar el fichero seleccionado.

Para el soporte que incluye Trac con *subversion*, algunas características adicionales
están disponibles:

 * Soporte para la propiedad ``svn:needs-lock``
 * Soporte para la propiedad ``svn:externals``

Vea También
===========

 * :ref:`Guía de Trac<TracGuide>`
 * :ref:`Conjunto de cambios en Trac<TracChangeset>`
 * :ref:`Permisos granulares en Trac<TracFineGrainedPermissions>`
