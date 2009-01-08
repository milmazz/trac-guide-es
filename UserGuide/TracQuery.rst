.. _TracQuery:

Ejecutando consultas personalizadas en el sistema de Tickets
============================================================

En adición a los :ref:`reportes <TracReports>`, Trac provee soporte para *consultas personalizadas sobre tickets*, usadas para desplegar la lista de tickets que cumplen con el conjunto de criterios especificados.

Para configurar y ejecutar las consultas personalizadas, vaya al módulo *Ver tickets* que se encuentra en la barra principal de navegación, seguidamente seleccione el enlace *Consulta Personalizada*.

Filtros
-------

Cuando usted vaya por primera vez a la página de consultas los filtros por omisión mostrarán todos los tickets abiertos, o si usted ya ha iniciado sesión en el sistema se le mostrarán los tickets abiertos que tiene asignados. Los filtros actuales pueden ser removidos al hacer click en el boton que se ubica a la derecha y que posee el signo negativo como etiqueta. Nuevos filtros pueden ser añadidos desde la lista desplegable que se ubica al fondo a la derecha de la caja de filtros. Los filtros que posean ya sea texto o un listado de opciones pueden ser agregados en múltiples ocasiones para aumentar el conjunto de criterios del tipo ``or``.

Usted puede usar los campos que se encuentran seguidos de la caja de filtros para agrupar los resultados en base a un campo, o mostrar la descripción completa para cada ticket.

Una vez que haya editado los filtros haga click en el botón *Actualizar* para refrescar los resultados.

Navegando tickets
-----------------

Haciendo click en uno de los resultados de la consulta lo llevará a ese ticket. Usted puede navegar a través de los resultados al hacer click en los enlaces *Ticket siguiente* o *Ticket previo* que se encuentran seguidamente debajo de la barra de navegación principal, o hacer click en el enlace *Regresar a consulta* para retornar a la página de consultas personalizadas.

Usted puede de manera segura editar cualquiera de los tickets y continuar navegando a través de los resultados obtenidos usando la serie de enlaces *Ticket siguiente/previo* o *Regresar a consulta* después de guardar los cambios. Si usted retorna a la página de consulta **cualquier ticket que haya sido editado** será mostrado en texto itálico. Si uno de los tickets que fue editado ya no coincide con la serie de criterios definidos se mostrará el texto correspondiente se mostrará en color gris. Por último, si un ticket ha sido creado y coincide con los criterios definidos en la página de consulta, el texto será mostrado en negrita.  

Los resultados de la página de consulta pueden actualizarse, a la vez eliminar estos indicadores de estado al hacer de nuevo click en el botón *Actualizar*.

Almacenando consultas
---------------------

Mientras tanto Trac no le permita almacenar consultas personalizadas y de alguna manera mostrar su disponibilidad en una lista navegable, usted puede guardar las referencias hacia dichas consultas personalizadas desde el contenido Wiki, tal como se describirá a continuación.

.. _UsingTracLinks:

Usando los enlaces de Trac
--------------------------

Usted probablemente desea almacenar algunas consultas de tal manera que las use posteriormente. Usted puede hacer esto al generar un enlace a la página de consultas personalizadas desde cualquier página Wiki.

.. code-block:: trac-wiki

   [query:status=new|assigned|reopened&version=1.0 Tickets activos para versión 1.0]

El cual es mostrado como:

   Ticket activos para versión 1.0

Lo anterior usa un lenguaje de consultas bastante sencillo para especificar los criterios de busqueda. Para mayor información continue leyendo más abajo.

Alternativamente, usted puede copiar la cadena de busqueda que muestra los resultados de la página de consultas personalizadas y luego llevarla hacia un enlace desde el Wiki, incluyendo el carácter ``?`` tal como se muestra a continuación:

.. code-block:: trac-wiki

   [query:?status=new&status=assigned&status=reopened&group=owner Tickets asignados agrupados por dueño]

Lo anterior se mostrará como:

  Ticket asignados agrupados por dueño

Usando el macro ``[[TicketQuery]]``
-----------------------------------

El macro ``TicketQuery`` le permite mostrar la lista de ticket que cumplen ciertos criterios donde sea que usted pueda usar el formato Wiki.

Ejemplo:

.. code-block:: trac-wiki

   [[TicketQuery(version=0.6|0.7&resolution=duplicate)]]

Lo cual mostrará algo como:

   Sin resultados

Tal como :ref:`Usando los enlaces de Trac <UsingTracLinks>`, el parámetro de este macro espera una cadena de consulta cuyo formato cumpla con las reglas del simple :ref:`lenguaje de consultas de tickets <QueryLanguage>`.

Una representación más compacta sin usar los sumarios de los tickets también se encuentra disponible:

.. code-block:: trac-wiki

   [[TicketQuery(version=0.6|0.7&resolution=duplicate, compact)]]

Lo cual mostrará algo como:

   Sin resultados

Finalmente si usted desea recibir solo el número de defectos que coinciden con una consulta puede hacerlo con el parámetro ``count``.

.. code-block:: trac-wiki
   
   [[TicketQuery(version=0.6|0.7&resolution=duplicate, count)]]

Lo cual mostrará algo como:

   0

.. _QueryLanguage:

Lenguaje de las consultas
-------------------------

Tanto enlaces de Trac ``query:`` como el macro ``[[TicketQuery]]`` usan un lenguaje de consultas reducido para especificar los filtros en las consultas. Básicamente, los filtros son separados por *ampersand* (``&``). Entonces cada filtro consiste del nombre del campo de un ticket, un operador, y uno o más valores. Más de un valor son separados por una tubería (``|``), esto significa que ese filtro deberá coincidir con cualquiera de los valores suministrados.

Los operadores disponibles son:

+----------+--------------------------------------------------------------------+
| Operador | Descripción                                                        |
+==========+====================================================================+
| ``=``    | El contenido del campo coincide exactamente con uno de los valores |
+----------+--------------------------------------------------------------------+
| ``~=``   | El contenido del campo contiene uno o más de los valores           |
+----------+--------------------------------------------------------------------+
| ``!^=``  | El contenido del campo comienza con uno de los valores             |
+----------+--------------------------------------------------------------------+
| ``$=``   | El contenido de campo finaliza con uno de los valores              |
+----------+--------------------------------------------------------------------+

Todos estos operadores pueden ser negados:

+----------+---------------------------------------------------------------+
| Operador | Descripción                                                   |
+==========+===============================================================+
| ``!=``   | El contenido del campo no coincide con ninguno de los valores |
+----------+---------------------------------------------------------------+
| ``!~=``  | El contenido del campo no contiene ninguno de los valores     |
+----------+---------------------------------------------------------------+
| ``!!^=`` | El contenido del campo no comienza con ninguno de los valores |
+----------+---------------------------------------------------------------+
| ``!$=``  | El contenido del campo no finaliza con ninguno de los valores |
+----------+---------------------------------------------------------------+

Vea También
-----------
 * :ref:`Tickets de Trac<TracTickets>`
 * :ref:`Reportes en Trac<TracReports>`
 * :ref:`Guía de Trac<TracGuide>`
