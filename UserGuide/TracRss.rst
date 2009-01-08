.. _TracRss:

Usando RSS con Trac
*******************

Muchos de los módulos de Trac soportan la sindicación de contenido usando el formato XML RSS (*Really Simple Syndication*). 

Usando la característica de subscripción al **RSS** en Trac, le permitirá seguir fácilmente el progreso del proyecto, ya sea un conjunto de inconformidades o incluso cambios en un simple archivo.

Trac soporta sindicación **RSS** en:

 * :ref:`Línea de Tiempo <TracTimeline>`, utilice la sindicación RSS para *subscribirse a los eventos del proyecto*. Mantengase informado acerca del progreso general del proyecto desde su visor favorito de RSS.
 * :ref:`Tickets <TracTickets>`, :ref:`Reportes <TracReports>` y :ref:`Consultas <TracQuery>`, permite sindicar tanto reportes así como resultados de consultas sobre el sistema de Tickets. Sea notificado acerca de inconformidades importantes y relevantes en el sistema de tickets.
 * Visor y Registro de revisiones, sindicación de cambios en archivos. Manténgase actualizado con los cambios en archivos o directorios específicos.

¿Cómo acceder a los datos RSS?
==============================

Donde sea que la sindicación RSS esté disponible en Trac, usted encontrará un pequeño ícono **XML** de color naranja, típicamente estará ubicado al fondo de la página. Haciendo click en el botón podrá acceder a la sindicación RSS para ese recurso en específico.

.. note::
  Diferentes módulos proveen diferentes datos en sus sindicaciones RSS. Usualmente, la información sindicada corresponde con la vista actual. Por ejemplo, si usted hace click en el enlace RSS de la página de reportes, la sindicación se basará en ese reporte. Esto puede ser explicado al pensar que la sindicación RSS es una *vista alternativa de los datos que actualmente son visualizados*. 

Enlaces
=======

 * `Especificación RSS <http://blogs.law.harvard.edu/tech/rss>`_.
 * `Mozilla Firefox <http://www.mozilla.org/products/firefox/>`_ soporta `marcadores en vivo <http://www.mozilla.org/products/firefox/live-bookmarks.html>`_ usando RSS.
 * `Sage <http://sage.mozdev.org>`_ es un agregador de RSS y Atom para Mozilla Firefox.
 * `KDE <http://kde.org>`_ `PIM <http://pim.kde.org/users.php>`_ es un lector de RSS para sistemas Linux/BSD/\*n\*x.
 * `Liferea <http://liferea.sourceforge.net/>`_ es un lector de RSS basado en GTK2 para Linux.
 * `Akregator <http://akregator.sourceforge.net/>`_ Es un lector de RSS para KDE, ahora es parte de KDE-PIM.
 * `WizzRSS <http://www.wizzrss.com/Welcome.php>`_ es un lector de *feeds* para Firefox.

Vea También
===========

 * :ref:`Referencia de Trac <TracGuide>`.
 * :ref:`Línea de tiempo <TracTimeline>`.
 * :ref:`Reportes <TracReports>`.
 * :ref:`Visualizador de código <TracBrowser>`.
