.. _TracChangeSet:

Manejo del conjunto de cambios
******************************

Trac incorpora en su sistema una funcionalidad para visualizar
diferencias o cambios en los ficheros.

Existen diferentes tipos de *conjunto de cambios*.
Algunos pueden corresponder a revisiones hechas en los repositorios,
otros pueden agregar cambios hechos en varias revisiones,
pero al final, cualquier tipo de diferencias pueden ser mostradas.

La vista del conjunto de cambios consiste en dos partes, la *cabecera*
y la *vista de diferencias*.

Cabecera del conjunto de cambios
================================

La cabecera muestra un resumen de todo el conjunto de cambios.
Acá podrá encontrar información tal como:

 * Estampas de tiempo -- Cuando fue enviado el conjunto de cambios
 * Autor -- Quien envio el conjunto de cambios
 * Mensaje -- Una breve descripción hecha por el autor (el registro de mensaje de envío)
 * Ficheros -- La lista de ficheros afectados por el conjunto de cambios.

Si más de una revisión está involucrada en el conjunto de cambios que está
siendo visualizado. Los campos de *estampa de tiempo*, *autor* y el *mensaje*
no serán mostrados.

Al lado de cada fichero listado, encontrará un rectángulo coloreado. El color
indica cómo el fichero fue afectado por el conjunto de cambios.

 * Verde: Agregado
 * Rojo: Removido
 * Amarillo: Modificado
 * Azul: Copiado
 * Gris: Movido

La leyenda de colores se localiza debajo de la cabecera como recordatorio.

Vista de diferencias
====================

Debajo de la cabecera se encuentra la parte principal del conjunto de cambios,
la vista de diferencias. Cada fichero es mostrado en una sección separada, cada una de
las cuales contendrá solo aquellas regiones del fichero que han sido afectadas por el 
conjunto de cambios. Existen dos estilos diferentes para mostrar las diferencias: *En 
línea* o *lado a lado*, puede cambiar entre estilos al usar el formulario de preferencias.

 * El estilo *en línea* muestra las regiones de cambios del fichero una debajo de la otra. Una región removida del fichero es coloreada en rojo, una región agregada será coloreada en verde. Si una región ha sido modificada, la versión anterior se mostrará encima de la nueva versión. Los números de línea ubicados a la izquierda indican la posición exacta del cambio tanto en la versión anterior como en la nueva versión del fichero.

.. note::
  **FIXME:** The ''inline'' style shows the changed regions of a file ''underneath'' each other. A region removed from the file will be colored red, an added region will be colored green. If a region was modified, the old version is displayed above the new version. Line numbers on the left side indicate the exact position of the change in both the old and the new version of the file.

 * El estilo *lado a lado* muestra la versión anterior en la parte izquierda y la nueva versión en la parte derecha (esto típicamente requiere mayor anchura que la vista en línea). Las regiones agregadas y removidas serán coloreadas de igual manera como el estilo en línea (verde y rojo, respectivamente), pero las regiones modificadas tendrán un fondo de color amarillo.

Adicionalmente, varias opciones avanzadas están disponibles en el 
formulario de preferencias para ajustar la visualización de las
diferencias:

 * Puede establecer cuantas líneas son mostradas tanto antes como después de cada cambio (si el valor *all* es usado, entonces el contenido completo del fichero será mostrado)
 * Usted puede activar o desactivar la visualización de líneas en blanco, cambios de casos y cambios en los espacios en blanco, esto le permitirá encontrar los cambios funcionales rápidamente.

.. note:: 
  **FIXME:** You can toggle whether blank lines, ''case changes'' and white space changes are ignored, thereby letting you find the functional changes more quickly

Diferentes vías para obtener las diferencias
============================================

Examinando el conjunto de cambios
---------------------------------

Cuando se encuentra viendo un envío al repositorio, como
cuando sigue un [wiki:TracLinks enlace] a un conjunto
de cambios o un evento en la [wiki:TracTimeline línea de tiempo],
Trac mostrará los cambios exactos hechos por el envío al repositorio.

También existen enlaces de navegación hacia el *Conjunto de cambios previo* y
*Siguiente conjunto de cambios*.

Examinando diferencias entre revisiones
---------------------------------------

Regularmente deseará ver los cambios hechos a un
fichero o a un directorio a través de múltiples revisiones.
La manera más fácil de obtener esto es desde el TracRevisionLog,
donde podrá seleccionar la *vieja* y la *nueva* revisión del fichero
o directorio, posteriormente debe dar clic en el botón *Ver Cambios*.

Examinando diferencias entre ramas
----------------------------------

Una de las características principales de los sistemas de control
de versiones es la posibilidad de trabajar simultáneamente en 
diferencias *líneas de desarrollo*, comúnmente denominadas *ramas*.
Trac permite que examine las diferencias exactas entre estas ramas.

Usando el botón **Ver cambios...** en el TracBrowser permitirá ingresar
el par de revisiones o rutas (path) en los campos *From:* y *To:*. El
conjunto de cambios resultantes consisten en los cambios que deben ser
aplicados al contenido ubicado en **From:** para obtener el contenido de **To:**.

Si lo considera conveniente, es posible invertir los roles *viejo* y *nuevo*
en el par de revisiones o rutas (path) al hacer clic en el enlace *Reverse Diff*
en la página del conjunto de cambios.

Revisando el último cambio
--------------------------

La última posibilidad de examinar cambios es usando el enlace *Last Change*
ubicado en el TracBrowser.

El enlace *Last Change* lo llevará al último cambio que fue realizado en esa ruta
o *path*. A partir de acá, podrá usar los enlaces *Previous Change* y *Next Change*
para hacerle seguimiento a la historia de cambios del fichero o directorio.

Vea también
===========

 * :ref:`Guía de Trac<TracGuide>`
 * :ref:`Visualizador de código<TracBrowser>`
