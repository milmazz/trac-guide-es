.. _TracReports:

Reportes en Trac
****************

El módulo de reportes de Trac provee una simple, pero poderosa
facilidad para generar reportes que presentan información acerca de
tickets en la base de datos de Trac.

En vez de tener un formato propio de definición de reportes, TracReports
confía en la sentencia ``SELECT`` del estándar SQL para la definición de
reportes personalizados.

.. note::
  El módulo de reportes ha entrado en fase de desuso en su forma actual puesto que seriamente limita la habilidad para el equipo de desarrollo de Trac para hacer ajustes al esquema bajo la base de datos. Los desarrolladores de Trac creen que :ref:`el módulo de consultas <TracQuery>` es un buen reemplazo que provee mayor flexibilidad y mejor usabilidad. Mientras existan ciertos reportes que no puedan ser manejados todavía por el módulo de consultas, se seguirá mejorando este módulo, hasta que en algún punto el módulo de reportes pueda ser removido completamente. Esto también significa que no habrán mayores mejoras en el módulo de reportes de ahora en adelante.

Usted puede reemplazar completamente el módulo de reportes por el
módulo de consultas simplemente deshabilitando el primero de ellos en
:ref:`trac.ini <TracIni>`:

.. code-block:: ini

  [components]
  trac.ticket.report.* = disabled

Esto hará que el módulo de consultas sea el manejador por omisión para
la sección *Ver Tickets*. Se le recomienda probar esta configuración
y reporte a los desarrolladores de Trac que tipo de características en
los reportes le hace falta o se está perdiendo, si existe alguna.

**En este punto se hace definitivamente necesario reiniciar su servidor
Web.**

Un reporte consiste en estas partes básicas:

 * **ID** -- Identificador único (secuencial)
 * **Título**  -- Título descriptivo
 * **Descripción**  -- Una breve descripción del reporte, soporta texto WikiFormatting.
 * **Cuerpo del reporte** -- Lista de resultados desde la consulta del reporte, acorde con el formato de los métodos descritos más abajo.
 * **Pie** -- Enlace a los formatos alternativos para la descarga de este reporte.

Cambiando el sentido de ordenamiento
====================================

Reportes simples, reportes sin agrupar para ser específicos, puede
cambiar el sentido de ordenamiento basado en cualquier columna
simplemente dando clic en la cabecera de una columna en particular.

Si una cabecera de columna es un hipernelace (roja), haciendo clic
en ella indica que quiere ordenarla tomándola como referencia. Haciendo
clic en la misma cabecera de nuevo revertirá el orden.

Cambiando la numeración de los reportes
=======================================

Pueden existir momentos en donde necesite cambiar el ID de un reporte,
posiblemente para organizar mejor sus reportes. Al presente esto
requiere un cambio en la base de datos de Trac. La tabla *report* posee
el siguiente esquema (como en 0.10):

 * id integer PRIMARY KEY
 * author text
 * title text
 * query text
 * description text

Cambiando el ID modifica el orden de visualización y el número en la
lista de *Reportes disponibles* y en el enlace permanente del reporte.
Esto se hace ejecutando una sentencia similar a la siguiente:

.. code-block:: sql

   update report set id=5 where id=3;

Tenga en mente que la integridad debe seguirse manteniendo (p.ej., el 
ID debe ser único, tampoco debe exceder el máximo, puesto que esto es
manejado por el sistema manejador de base de datos en algún lado).

Navegando tickets
=================

Haciendo clic en uno de los resultados del reporte lo llevará a ese
ticket. Puede navegar a través de los resultados haciendo clic en los
enlaces *Next ticket* o *Previous ticket* que se encuentran debajo de
la barra del menú principal, o haciendo clic en el enlace *Back to
report* para retornar a la página del reporte.

Podrá editar de manera segura cualquiera de los tickets y continuar
navegando a través de los resultados usando los enlaces 
"Next/Previous/Back to report" después de guardar los cambios, pero
cuando retorne al reporte, no existirá un indicio o pista acerca de lo
que ha cambiado, tal como si estuviese navegando una lista de tickets
obtenida a partir de una consulta (vea TracQuery#NavigatingTickets). *(a partir de 0.11)*

Formatos alternativos para descarga
===================================

Aparte de la vista por omisión en HTML, los reportes también pueden
exportarse a un número determinado de formatos alternativos.
Al final de la página de reportes, encontrará una lista de los formatos
de datos disponibles. Haga clic en el enlace deseado para descargar el
formato alternativo del reporte.

Delimitado por comas - CSV (Valores separados por Comas)
--------------------------------------------------------

Exporta el reporte en texto sin formato, cada fila en su propia línea,
las columnas están separadas por una coma (``,``).

.. note::
  Retornos de carro, FIXME:line feeds, y comas son eliminados de la columna de datos para preservar la estructura del CSV.

Delimitado por tabulaciones
---------------------------

Similar al de arriba, pero usando tabulaciones (``\t``) en vez de
comas.

RSS - Sindicación de contenido en XML
-------------------------------------

Todos los reportes soportan sindicación usando XML/RSS 2.0. Para 
subscribirse a un feed RSS, haga clic en el ícono color naranja *XML*
que se encuentra al final de la página. Vea TracRss para información
general acerca del soporte RSS en Trac. 

Creando reportes personalizados
===============================

*La creación de reportes personalizados requiere de un conocimiento
moderado de SQL.*

Un reporte es básicamente una consulta SQL, ejecutada y presentada por
Trac. Los reportes pueden ser vistos y creados a partir de una
expresión SQL personalizada directamente desde la interfaz Web.

FIXME: A report is basically a single named SQL query, executed and presented by
Trac.  Reports can be viewed and created from a custom SQL expression directly
in from the web interface.

Típicamente, un reporte consiste de una expresión ``SELECT`` a la tabla
*ticket*, usando las columnas disponibles y ordenándolas de la manera
que desee.

Columnas de ticket
==================

La tabla *ticket* tiene las siguientes columnas:

 * id
 * type
 * time
 * changetime
 * component
 * severity  
 * priority 
 * owner
 * reporter
 * cc
 * version
 * milestone
 * status
 * resolution
 * summary
 * description
 * keywords

Vea TracTickets para una detallada descripción de los campos de las
columnas.

**Ejemplo:** *todos los tickets activos, ordenados por prioridad y
tiempo de creación*

.. code-block:: sql

  SELECT id AS ticket, status, severity, priority, owner, 
       time as created, summary FROM ticket 
  WHERE status IN ('new', 'assigned', 'reopened')
  ORDER BY priority, time

Reportes avanzados: Variables dinámicas
=======================================

Para reportes más flexibles, Trac soporta el uso de *variables 
dinámicas* en las sentencias SQL de los reportes.
Brevemente, las variables dinámicas son cadenas *especiales* que son
reemplazadas por datos personalizados antes de la ejecución de la
consulta.

Usando variables en una consulta
--------------------------------

La sintaxis para variables dinámicas es simple, cualquier palabra en
mayúsculas que comience con ``$`` es considerada una variable.

Ejemplo:

.. code-block:: sql

   SELECT id AS ticket,summary FROM ticket WHERE priority=$PRIORITY

Para asignarle un valor a la variable ``$PRIORITY`` cuando está viendo
el reporte, debe definirlo como un argumento en la URL del reporte,
dejando de lado el ``$``.

Ejemplo:

   http://trac.edgewall.org/reports/14?PRIORITY=high

Para usar múltiples variables, separe cada una de ellas con un ``&``.

Ejemplo:

   http://trac.edgewall.org/reports/14?PRIORITY=high&SEVERITY=critical

Variables especiales/constantes
-------------------------------

Existe una variable dinámica *mágica* que permite crear reportes
prácticos, su valor automáticamente se establece sin tener que cambiar
la URL.

 * ``$USER`` -- Almacena el *nombre de usuario* de aquel usuario que ha iniciado sesión.

Ejemplo: *Listar todos los tickets asignados a mí*

.. code-block:: sql

   SELECT id AS ticket,summary FROM ticket WHERE owner=$USER

Reportes avanzados: Formato personalizado
=========================================

Trac también es capaz de reportes más avanzados, incluyendo *layouts*
personalizados, agrupamiento de resultados y estilos CSS definidos por
el usuario. Para crear estos reportes, use sentencias SQL 
especializadas para controlar la salida del motor de reportes de Trac.

Columnas especiales
===================

Para darle formato a los reportes, TracReports busca nombres de
columnas *mágicas* en los resultados de las consultas. Estos nombres
*mágicos* son procesados y afectan el *layout* y el estilo del reporte
final.

Formato automático de columnas
------------------------------

 * **ticket** -- Número ID del ticket. Se convierte en un hiperenlace hacia ese ticket.
 * **created, modified, date, time** -- Da formato a las celdas como una fecha y/u hora.
 * **description** -- Campo de descripción del ticket, analizado a través del motor Wiki.

**Ejemplo:**

.. code-block:: sql

   SELECT id as ticket, created, status, summary FROM ticket 

Formato personalizado de columnas
---------------------------------

Aquellas columnas cuyos nombres comienzan y finalizan con dos
caracteres de subrayado (Ejemplo: ```__color__```) son asumidas como
*pistas de formato*, afectando la apariencia de la fila.
 
 * ```__group__``` -- Agrupa los resultados en base a valores en esta columna. Cada grupo tendrá su propia cabecera y tabla.
 * ```__color__``` -- Debe ser un valor numérico en el rango desde 1 a 5 para seleccionar un color de fila predefinido. Típicamente usado para colorear las filas por prioridad del *issue*.

FIXME: Convertir a formato rst.
... <div style="margin-left:7.5em">Defaults: 
... <span style="border: none; color: #333; background: transparent;  font-size: 85%; background: #fdc; border-color: #e88; color: #a22">Color 1</span>
... <span style="border: none; color: #333; background: transparent;  font-size: 85%; background: #ffb; border-color: #eea; color: #880">Color 2</span>
... <span style="border: none; color: #333; background: transparent;  font-size: 85%; background: #fbfbfb; border-color: #ddd; color: #444">Color 3</span>
... <span style="border: none; color: #333; background: transparent; font-size: 85%; background: #e7ffff; border-color: #cee; color: #099">Color 4</span>
... <span style="border: none; color: #333; background: transparent;  font-size: 85%; background: #e7eeff; border-color: #cde; color: #469">Color 5</span>

 * ```__style__``` -- Una expresión de estilo CSS personalizado a ser usado en la fila actual.

**Ejemplo:** *Lista de tickets activos, agrupados por hito, coloreados por prioridad*

.. code-block:: sql

  SELECT p.value AS __color__,
     t.milestone AS __group__,
     (CASE owner WHEN 'daniel' THEN 'font-weight: bold; background: red;' ELSE '' END) AS __style__,
       t.id AS ticket, summary
  FROM ticket t,enum p
  WHERE t.status IN ('new', 'assigned', 'reopened') 
    AND p.name=t.priority AND p.type='priority'
  ORDER BY t.milestone, p.value, t.severity, t.time

.. note::
  Una unión o *join* de tablas es usado para fusionar las prioridades del *ticket* con su representación numérica desde la tabla *enum*.

Cambiando el *layout* de las filas en los reportes
--------------------------------------------------

Por omisión, todas las columnas en cada fila son mostradas en una simple
fila en el reporte en formato HTML, posiblemente formateado acorde a las
descripciones de arriba. Sin embargo, también es posible crear entradas
multilínea en los reportes.

 * ```column_``` -- *Rompe la fila después de esto*. Al agregar un caracter de subrayado (``_``) al nombre de la columna, las columnas restantes continuarán en una segunda línea.
 * ```_column_``` -- *Fila completa*. Al agregar un caracter de subrayado (``_``) tanto al iniciao como al final del nombre de una columna, los datos serán mostrados en una fila separada.
 * ```_column```  --  *Ocultar datos*. Al colocar un caracter de subrayado (``_``) como prefijo en el nombre de una columna se le instruye a Trac para que oculte el contenido de la salida HTML. Esto es útil para información que será visible solo si es descargada en otros formatos (tal como CSV o RSS/XML).

**Ejemplo:** *Lista de tickets activos, agrupados por hito, coloreados por prioridad, con descripción y un *layout* de múltiples líneas*

.. code-block:: sql

  SELECT p.value AS __color__,
       t.milestone AS __group__,
       (CASE owner 
          WHEN 'daniel' THEN 'font-weight: bold; background: red;' 
          ELSE '' END) AS __style__,
       t.id AS ticket, summary AS summary_,             -- ## Rompa línea acá
       component,version, severity, milestone, status, owner,
       time AS created, changetime AS modified,         -- ## Fecha con formato
       description AS _description_,                    -- ## Use una fila completa
       changetime AS _changetime, reporter AS _reporter -- ## Oculte de la salida HTML
  FROM ticket t,enum p
  WHERE t.status IN ('new', 'assigned', 'reopened') 
    AND p.name=t.priority AND p.type='priority'
  ORDER BY t.milestone, p.value, t.severity, t.time

Reportando sobre campos personalizados
--------------------------------------

Si ha agregado campos personalizados a sus tickets (una característica
presente desde la v0.8, vea TracTicketsCustomFields), puede escribir
consultas SQL que agrupe dichos campos. Necesitará hacer una unión o
*join* con la tabla ``ticket_custom``, pero esto no es especialmente
sencillo.

Si usted tiene tickets en la base de datos *antes* de haber declarado
los campos adicionales en el trac.ini, no existirán datos asociados en
la tabla ``ticket_custom``. Para trabajar alrededor de esto, utilice
la clausula SQL ``LEFT OUTER JOIN``. Vea TracIniReportCustomFieldSample
para algunos ejemplos.

**Note que necesita establecer los permisos necesarios para ver los
botones para añadir o editar reportes.** 

Vea también
===========

 * :ref:`Tickets de Trac<TracTickets>`
 * :ref:`Consultas en Trac<TracQuery>`
 * :ref:`Guía de Trac<TracGuide>`
 * `Query Language Understood by SQLite <http://www.sqlite.org/lang_expr.html>`_
