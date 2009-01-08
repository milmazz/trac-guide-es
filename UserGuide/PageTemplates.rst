.. _PageTemplates:

Plantilla de páginas Wiki
*************************

Esta característica se encuentra presente desde Trac `0.11 <http://trac.edgewall.org/milestone/0.11>`_

El contenido por omisión para una nueva página del Wiki puede elegirse
a partir de una lista de páginas plantilla. 

Esta lista se genera a partir de todas las páginas wiki existentes que
tienen un nombre que comienza por ``PageTemplates/``

El contenido inicial de una nueva página será el contenido de la página
plantilla elegida, o una página en blanco si la entrada especial *(blank
page)* es seleccionada. Cuando no existen páginas wiki que coincidan con
ese prefijo, el contenido inicial siempre será una página en blanco y la
lista desplegable de páginas plantilla no se mostrará (Por ejemplo, esto es 
similar al comportamiento que se tiene en una nueva instalación de Trac).

Para crear una nueva plantilla, simplemente cree una nueva página que
tenga un nombre que comience con ``PageTemplates/``

.. note::
 Puede incluso crear la página ``PageTemplates/Template`` para facilitar la creación de nuevas páginas plantilla.

Para visualizar la lista de plantillas disponibles puede hacer uso del
macro ``[[TitleIndex(PageTemplates/)]]``

Vea también: :ref:`Wiki de Trac<TracWiki>`
