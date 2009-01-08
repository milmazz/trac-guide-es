.. _WikiMacros:

= Trac Macros =

[[PageOutline]]

Trac macros are plugins to extend the Trac engine with custom 'functions' written in Python. A macro inserts dynamic HTML data in any context supporting WikiFormatting.

Another kind of macros are WikiProcessors. They typically deal with alternate markup formats and representation of larger blocks of information (like source code highlighting).

== Using Macros ==
Macro calls are enclosed in two ''square brackets''. Like Python functions, macros can also have arguments, a comma separated list within parentheses. 

Trac macros can also be written as TracPlugins. This gives them some capabilities that macros do not have, such as being able to directly access the HTTP request.

=== Example ===

A list of 3 most recently changed wiki pages starting with 'Trac':

{{{
 [[RecentChanges(Trac,3)]]
}}}

Display:
 [[RecentChanges(Trac,3)]]

== Available Macros ==

''Note that the following list will only contain the macro documentation if you've not enabled `-OO` optimizations, or not set the `PythonOptimize` option for [wiki:TracModPython mod_python].''

[[MacroList]]

== Macros from around the world ==

The [http://trac-hacks.org/ Trac Hacks] site provides a wide collection of macros and other Trac [TracPlugins plugins] contributed by the Trac community. If you're looking for new macros, or have written one that you'd like to share with the world, please don't hesitate to visit that site.

== Developing Custom Macros ==
Macros, like Trac itself, are written in the [http://python.org/ Python programming language].

For more information about developing macros, see the [wiki:TracDev development resources] on the main project site.


== Implementation ==

Here are 2 simple examples showing how to create a Macro with Trac 0.11. 

Also, have a look at [trac:source:tags/trac-0.11/sample-plugins/Timestamp.py Timestamp.py] for an example that shows the difference between old style and new style macros and at the [trac:source:tags/trac-0.11/wiki-macros/README macros/README] which provides a little more insight about the transition.

=== Macro without arguments ===
It should be saved as `TimeStamp.py` as Trac will use the module name as the Macro name
{{{
#!python
from datetime import datetime
# Note: since Trac 0.11, datetime objects are used internally

from genshi.builder import tag

from trac.util.datefmt import format_datetime, utc
from trac.wiki.macros import WikiMacroBase

class TimeStampMacro(WikiMacroBase):
    """Inserts the current time (in seconds) into the wiki page."""

    revision = "$Rev$"
    url = "$URL$"

    def expand_macro(self, formatter, name, args):
        t = datetime.now(utc)
        return tag.b(format_datetime(t, '%c'))
}}}

=== Macro with arguments ===
It should be saved as `HelloWorld.py` (in the plugins/ directory) as Trac will use the module name as the Macro name
{{{
#!python
from trac.wiki.macros import WikiMacroBase

class HelloWorldMacro(WikiMacroBase):
    """Simple HelloWorld macro.

    Note that the name of the class is meaningful:
     - it must end with "Macro"
     - what comes before "Macro" ends up being the macro name

    The documentation of the class (i.e. what you're reading)
    will become the documentation of the macro, as shown by
    the !MacroList macro (usually used in the WikiMacros page).
    """

    revision = "$Rev$"
    url = "$URL$"

    def expand_macro(self, formatter, name, args):
        """Return some output that will be displayed in the Wiki content.

        `name` is the actual name of the macro (no surprise, here it'll be
        `'HelloWorld'`),
        `args` is the text enclosed in parenthesis at the call of the macro.
          Note that if there are ''no'' parenthesis (like in, e.g.
          [[HelloWorld]]), then `args` is `None`.
        """
        return 'Hello World, args = ' + unicode(args)
    
    # Note that there's no need to HTML escape the returned data,
    # as the template engine (Genshi) will do it for us.
}}}


=== {{{expand_macro}}} details ===
{{{expand_macro}}} should return either a simple Python string which will be interpreted as HTML, or preferably a Markup object (use {{{from trac.util.html import Markup}}}).  {{{Markup(string)}}} just annotates the string so the renderer will render the HTML string as-is with no escaping. You will also need to import Formatter using {{{from trac.wiki import Formatter}}}.

If your macro creates wiki markup instead of HTML, you can convert it to HTML like this:

{{{
#!python
  text = "whatever wiki markup you want, even containing other macros"
  # Convert Wiki markup to HTML, new style
  out = StringIO()
  Formatter(self.env, formatter.context).format(text, out)
  return Markup(out.getvalue())
}}}
