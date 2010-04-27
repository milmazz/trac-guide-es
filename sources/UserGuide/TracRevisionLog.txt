.. _TracRevisionLog:

Hitórico de revisiones
**********************

Cuando navega el repositorio, siempre es posible consultar la vista de
*histórico de revisiones* correspondiente a la ruta que actualmente
está viendo. Esto le mostrará una lista de los conjuntos de cambios más
recientes en los cuales la ruta actual o sus descendientes hayan sido
modificados.

El formulario del histórico de revisiones
=========================================

Es posible establecer la revisión a partir de la cual el histórico
de revisiones deberá comenzar, usando el campo *View log starting
at*. Un valor vacío o un valor *head* es tomado como el conjunto
de cambios más reciente.

También es posible especificar la revisión en la cual el histórico
de revisiones deberá detenerse, usando el campo *back to*. Por
omisión, si es dejado vacío, significa que el histórico de revisiones
se detendrá tan pronto como se hayan listado 100 revisiones.

Además, existen tres modos de operación del histórico de revisiones.

Por omisión, el histórico de revisiones *stops on copy*, esto significa
que siempre que se detecte una operación *Agregar*, *Copiar* o 
*Renombrar*, no se mostrará una revisión previa. Esto es muy
conveniente cuando se trabaja con ramas, puesto que se observa la
historia correspondiente a aquello hecho en la rama.

También es posible indicar que se desea ver que sucedió antes de una
operación *Copiar* o *Renombrar*, seleccionando el modo *Follow
copies*. Esto pasará todos los cambios hechos al copiar o renombrar.
Cada vez que el nombre de la ruta o *path* cambie, existirá un nivel
de indentación adicional. De esa manera, los cambios en las diferentes
rutas son fácilmente agrupadas visualmente.

Además es también posible pasar a través de los cambios hechos por la
operación *Agregar*, esto permitiría ver si existió algún cambio hecho
por la operación *Borrar* en esa ruta, antes de *Agregar*. Este modo
corresponde al modo denominado *Show only adds, moves and deletes*.
Mientras que este modo puede resultar útil algunas veces, tenga cuidado
al usarlo puesto que esta operación requiere de recursos de manera
intensiva.

Finalmente, también existe la casilla de verificación *Show full log
messages*, la cual controla si el contenido completo del registro de
mensaje de envío debe mostrarse para cada cambio, o si solamente debe
mostrarse una versión reducida de los mismos.

La información del histórico de revisiones
==========================================

Para cada entrada del histórico de revisiones, se muestran 7 columnas:

 1. La primera columna contiene un par de botones de radio que deben
    ser usados para seleccionar la *vieja* y la *nueva* revisión que
    será usada en [wiki:TracRevisionLog#viewingtheactualchanges ver
    los cambios actuales].
 2. Una leyenda de colores (similar a la usada para el
    [wiki:TracChangeset#ChangesetHeader conjunto de cambios]) que
    indica el tipo de cambio.
    Haciendo clic en esta columna recarga el histórico de revisiones
    así que se reinicia con este cambio.
 3. La **Fecha** en la que el cambio se realizó.
 4. El número de la **Revisión**, mostrado como `@xyz`.
    Esto es un enlace al TracBrowser, usando dicha revisión como la
    línea base.
 5. El número del **Conjunto de cambios**, mostrado como `[xyz]`.
    Esto es un enlace a la vista de TracChangeset.
 6. El **Autor** del cambio.
 7. El **Mensaje de registro**, el cual puede contener un sumario o el
    mensaje completo del registro de envío, esto depende del valor de
    la casilla de verificación *Show full log messages* que se muestra
    en el formulario superior.

Inspeccionando los cambios entre revisiones
===========================================

Los botones *View changes...* (ubicados arriba y abajo de la lista de
cambios, en el lado izquierdo) mostraran el conjunto de diferencias
correspondientes a los cambios agregados a partir de la revisión 
*vieja* (primer botón de radio) hasta la *nueva* revisión (segundo
botón de radio), en la vista de TracChangeset.

Note que la revisión *vieja* no necesariamente debe ser anterior a la
revisión *nueva*, simplemente da una base para establecer la 
diferencia. Por lo tanto, fácilmente es posible generar un *diferencia
reversa*, esto con el fin de revertir todo aquello que se ha hecho en el
rango de revisiones indicadas.

Finalmente, si las dos revisiones son idénticas, el correspondiente
conjunto de cambios será mostrado (mismo efecto que al hacer clic en la
columna 5).

Formatos alternativos
=====================

El texto del histórico de cambios
---------------------------------

Al final de la página, existe un enlace *ChangeLog* que le mostrará el
rango de revisiones tal como se le muestra actualmente en la página,
pero como texto sin formato, haciendo uso de las convenciones para los
ficheros de históricos de cambios o ChangeLog.

Soporte RSS
-----------

El histórico de cambios también provee un *feed* **RSS** que permite
hacerle seguimiento a los cambios. Para subscribirse a un *feed*, ya
sea para un archivo o un directorio, abra el histórico de revisiones en
el navegador y haga clic en el ícono naranja *XML* que se encuentra al
final de la página. Para mayor información del :ref:`soporte RSS en Trac<TracRss>`.

Vea también
===========

 * :ref:`Visualizador de código<TracBrowser>`
 * :ref:`Conjunto de cambios en Trac<TracChangeset>`
 * :ref:`Guía de Trac<TracGuide>`
