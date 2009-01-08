.. _WikiPageNames:

Nombres de las páginas Wiki
***************************

Los nombres de las páginas Wiki comúnmente usan la convención
CamelCase. Dentro del texto wiki, cualquier palabra en CamelCase
automáticamente se convierte en un hiperenlace hacia la página wiki con
ese nombre.

Los nombres de páginas en CamelCase deben seguir las siguientes reglas:

 1. El nombre debe consistir de **caracteres alfabéticos solamente**. No son permitidos los digitos, espacios, signos de puntuación o signos de subrayado.
 2. El nombre debe al menos contener dos letras mayúsculas.
 3. El primer caracter debe ser mayúscula.
 4. Cualquier letra mayúscula debe estar seguida por una o más letras en minúscula.
 5. El uso de la barra o *slash* (``/``) es permitido en los nombres de las páginas (posiblemente representando jerarquía).

Si desea crear una página wiki que no sigue las reglas CamelCase puede
usar la siguiente sintaxis:

 * [wiki:Wiki_page], [wiki:ISO9000]
 * [wiki:"El Espacio Importa"] esta nombre de página incluye caracteres de espacio
 * o simplemente: ["NombrePaginaWiki"]s (MoinMoin's internal free links style)

Esto sería representado como:

 * [wiki:Wiki_page], [wiki:ISO9000]
 * [wiki:"Space Matters"] that page name embeds space characters
 * or simply: ["WikiPageName"]s (!MoinMoin's internal free links style)

A partir de Trac 0.11, también es posible enlazar a una *versión*
específica de una página Wiki, así como haría con una versión
específica de un fichero, por ejemplo: WikiStart@1

Vea también TracLinks#QuotingspaceinTracLinks.

Finalmente, tal como se muestra en la línea de arriba, también puede
agregar un *ancla* al nombre de una página Wiki, con el fin de enlazar
con una sección específica dentro de esa página. El ancla puede verse fácilmente
al colocar el cursor del ratón encima del encabezado de la sección,
luego al hacer clic en el signo de párrafo [[html(&para;)]] que
aparece al final. El ancla usualmente es generado automáticamente, pero
también es posible especificarlo de manera explícita. Para mayor
información sobre este último punto vea 
WikiFormatting#using-explicit-id-in-heading.

Vea También: 

 * :ref:`Pasos para crear una página Wiki<WikiNewPage>`
 * :ref:`Formato del wiki<WikiFormatting>`
 * :ref:`El Wiki de Trac<TracWiki>`
 * :ref:`Enlaces en Trac<TracLinks>`
