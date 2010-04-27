.. _TracTickets:

El sistema de tickets de Trac
*****************************

La base de datos de tickets de Trac provee un simple pero efectivo
sistema de seguimiento de *issues* y errores de programación dentro de
un proyecto.

Como elemento central de Trac para el manejo del proyecto, los tickets
son usados para *tareas del proyecto*, *solicitud de características*,
*reporte de errores* y *issues de soporte del software*.

Al igual que el :ref:`Sistema Wiki<TracWiki>`, este subsistema ha sido
diseñado con el propósito de permitir que la contribución y la
participación de los usuarios sea tan sencilla como sea posible.
Debería ser muy sencillo reportar errores, realizar preguntas y sugerir
mejoras en el sofware.

Un *issue* es asignado a la persona quien debería resolverlo o
reasignar el ticket a alguien más.
Todos los tickets pueden editarse, anotarse, asignarse, darle prioridad
y discutirlos en cualquier momento.

Campos de los tickets
=====================

Un ticket debe contener los siguientes atributos de información:
 
 * **Reporter** - El autor del ticket.
 * **Type** - La naturaleza del ticket (por ejemplo, defecto o solicitud de mejora)
 * **Component** - El módulo del proyecto o el subsistema que a este ticket le concierne.
 * **Version** - Versión del proyecto a la que este ticket pertenece.
 * **Keywords** - Palabras claves con las que el ticket es etiquetado. Útil para búsquedas y generación de reportes.
 * **Priority** - La importancia de este *issue*, desde el rango *trivial* a *bloqueante*.
 * **Hito** - Cuando este *issue* debería ser resuelto como máximo.
 * **Assigned to/Owner** - Personal que funge de principal responsable para el manejo/resolución de este *issue*.
 * **Cc** - Una lista separada por comas de otros usuarios o direcciones de correo electrónico a notificar. *Note que esto no implica responsabilidad o cualquier otra política*.
 * **Resolution** - Razón por la cual el ticket fue cerrado: ``fixed``, ``invalid``, ``wontfix``, ``duplicate``, ``worksforme``.
 * **Status** - ¿Cual es el estado actual? Uno de ``new``, ``assigned``, ``closed``, ``reopened``.
 * **Summary** - Una breve descripción que indica de manera concisa el problema o *issue*.
 * **Description** - El cuerpo del ticket. Una buena descripción debe ser específica, descriptiva e ir al punto principal.

.. note::
  Versiones de Trac previas a la 0.9 no contaban con el campo *type*, en vez de ello se proveía un campo *severity* y diferentes valores para el campo *priority*. Este cambio fue hecho para simplificar el modelo de los ticket removiendo la no muy clara distinción entre *priority* y *severity*. Sin embargo, el viejo modelo todavía está disponible si lo prefiere: Simplemente agregue/modifique los valores por omisión de *priority* y *severity*, opcionalmente oculte el campo *type* al remover todos sus posibles valores a través del comando :ref:`trac-admin<TracAdmin>`.

.. note::
  Los campos :ref:`type<TicketTypes>`, :ref:`component<TicketComponent>`, version, priority y severity pueden ser manejados con :ref:`trac-admin<TracAdmin>` o con el complemento WebAdmin.

.. note::
  La descripción de los valores por omisión del campo *priority* puede encontrarla en :ref:`<TicketTypes#Whyistheseverityfieldgone>`

  FIXME: Description of the builtin ''priority'' values is available at [wiki:TicketTypes#Whyistheseverityfieldgone]

Cambiando y comentando tickets
==============================

Una vez que un ticket ha ingresado al sistema Trac, en cualquier
momento puede cambiar la información al hacer una **anotación** sobre
el reporte. Esto significa que los cambios y los comentarios al ticket
son registrados como parte del ticket mismo.

Cuando ve un ticket, la historia de cambios aparecerá debajo del área
principal del ticket.

*En el proyecto de Trac, se utilizan los comentarios para discutir los
**issues** y tareas. Esto hace entender de manera más fácil la motivación 
de la elección detrás del diseño o la implementación, cuando se retorna
a él posteriormente.*

.. note::
  Una importante característica es la posibilidad de usar :ref:`enlaces<TracLinks>` y el :ref:`formato Wiki<WikiFormatting>` en la descripción y los comentarios de los tickets. Utilice los :ref:`enlaces de Trac<TracLinks>` para referirse a otros *issues*, conjuntos de cambios o ficheros para hacer más específico su ticket y más fácil de comprender.

.. note::
  Vea :ref:`Notificaciones en Trac<TracNotification>` para conocer como configurar las notificaciones vía correo electrónico acerca de los cambios en los tickets.

.. note::
  Vea :ref:`el flujo de Trac<TracWorkflow>` para información acerca de los estados de transiciones (ciclo de vida del ticket), y como puede personalizar dicho flujo de trabajo o *workflow*.

Valores por defecto para campos de listas desplegables
======================================================

La opción seleccionada por omisión para varios campos de listas
desplegables pueden ser establecidos en el fichero
:ref:`trac.ini<TracIni>`, en la sección ``[ticket]``:

 * ``default_component``: Nombre del componente seleccionado por omisión
 * ``default_milestone``: Nombre del hito por omisión
 * ``default_priority``: Valor por omisión de la prioridad
 * ``default_severity``: Valor por omisión de la severidad
 * ``default_type``: Tipo por omisión del ticket
 * ``default_version``: Nombre de la versión por omisión

Si cualquiera de estas opciones es omitida, el valor por omisión puede
ser el primero en la lista, o un valor vacío, dependiendo si es 
requerido que el campo esté establecido.

Ocultando campos y agregando campos personalizados
==================================================

Muchos de los campos por omisión de los tickets pueden ser ocultados
desde la interfaz web simplemente removiendo todos los posibles valores
a través de :ref:`trac-admin<TracAdmin>`. Esto por supuesto aplica 
solamente en campos con listas desplegables, como *type*, *priority*,
*severity*, *component*, *version* y *milestone*.

Trac también permite agregar campos personalizados a los tickets. Vea
:ref:`Campos personalizados en tickets<TracTicketsCustomFields>` para
mayor información al respecto.

Campo *Assign-to* como lista desplegable
========================================

Si la lista de los posibles responsables de los tickets es finita,
puede cambiar el campo de los tickets *assign-to* de entrada de texto
a una lista desplegable. Esto lo puede hacer al establecer la opción
``restrict_owner`` en la sección ``[ticket]`` en el fichero 
:ref:`trac.ini<TracIni>` a ``true``. En ese caso, Trac usará la lista de
todos los usuarios que han accedido al proyecto para generar el campo
como lista desplegable.

Para aparecer en la lista desplegable, el usuario necesita estar
registrado en el proyecto, por ejemplo, una sesión de usuario debe
existir en la base de datos. Tal entrada es automáticamente creada en
la base de datos la primera vez que el usuario envía un cambio al
proyecto, por ejemplo cuando está editando los detalles del usuario en
la página de *Settings*, o simplemente al autenticarse si el usuario
posee una cuenta. Además, el usuario debe poseer el
:ref:`permiso<TracPermissions>` ``TICKET_MODIFY``.

.. note::
  Vea `Populating Assign To Drop Down <http://pacopablo.com/wiki/pacopablo/blog/set-assign-to-drop-down>`_ para conocer como agregar entradas de usuarios a nivel de base de datos.

Valores preestablecidos para nuevos tickets
===========================================

Para crear un enlace al formulario de nuevo ticket con valores
predefinidos, necesita usar la URL ``/newticket?`` con
``variable=valor`` separados por ``&`` 

Las posibles variables son:

 * **type** - Lista desplegable de tipo
 * **reporter** - Nombre o dirección de correo electrónico del autor del ticket
 * **summary** - Línea de sumario del ticket
 * **description** - Descripción larga del ticket
 * **component** - Lista desplegable de componente
 * **version** - Lista desplegable de versión
 * **severity** - Lista desplegable de severidad
 * **keywords** - Palabras claves
 * **priority** - Lista desplegable de prioridad
 * **milestone** - Lista desplegable de hitos
 * **owner** - Persona responsable por el ticket
 * **cc** - Lista de direcciones de correo electrónico o usuarios para notificar acerca de los cambios en el ticket

**Ejemplo:** ``/newticket?summary=Compile%20Error&version=1.0&component=gui``

Vea también:  

 * :ref:`Guía Trac<TracGuide>`
 * :ref:`Wiki de Trac<TracWiki>`
 * :ref:`Campos personalizados en los tickets de Trac<TracTicketsCustomFields>`
 * :ref:`Notificaciones en Trac<TracNotification>`
 * :ref:`Reportes en Trac<TracReports>`
 * :ref:`Consultas en Trac<TracQuery>`
