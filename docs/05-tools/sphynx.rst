Style guide
===========

Headers
-------

.. code-block:: rst

    Title (H1)
    ==========

    Section heading (H2)
    --------------------

    Subsection heading (H3)
    ^^^^^^^^^^^^^^^^^^^^^^^

Inline Markup
-------------

Surround text with:

- One asterisk for \*emphasis\* (*italics*)
- Two asterisks for \**strong emphasis\** (**bold**)
- Two backticks for \``code samples``\ (an ``<html>`` element)

Links
-----

.. code-block:: rst

  Search it in `Google <https://www.google.com>`_.

Search it in `Google <https://www.google.com>`_.

Lists
-----

Lists can be started with a ``-`` or ``*`` character:

.. code-block:: rst

  - This is one item
  - This is a second item

Numbered lists can start with a number, or they can be auto numbered by starting each item with the \# character. Please use the \# syntax.

.. code-block:: rst

  1. Numbered list item one.(don't use numbers)
  2. Numbered list item two.(don't use numbers)

  #. Auto-numbered one.
  #. Auto-numbered two.

Source code
-----------

Source code is very commonly included in these articles. Images should never be used to display source code. Prefer ``literalinclude`` for most code samples. Reserve ``code-block`` for small snippets that are not included in the sample project. A ``code-block`` can be declared as shown below, including spaces, blank lines, and indentation:

.. code-block:: rst

  .. code-block:: c#

  public void Foo()
  {
    // Foo all the things!
  }

This results in:

.. code-block:: c#

  public void Foo()
  {
    // Foo all the things!
  }

`List of all available lexers <http://pygments.org/docs/lexers/>`_

Images
------

Images such as screen shots and explanatory figures or diagrams should be placed in a ``_static`` folder within a folder named the same as the article file. References to images should therefore always be made using relative references, e.g. ``article-name/style-guide/_static/asp-net.png``. Note that images should always be saved as all lower-case file names, using hyphens to separate words, if necessary.

.. note:: Do not use images for code. Use ``code-block`` or ``literalinclude`` instead.

To include an image in an article, use the ``.. image`` directive:

.. code-block:: rst

  .. image:: ../_static/ateam.png

.. note:: No quotes are needed around the file name.

Here's an example using the above syntax:

.. image:: ../../common/_static/ateam.png

Images are responsively sized according to the browser viewport when using this directive. Currently the maximum width supported by the https://docs.asp.net theme is 697px.

Notes
-----

To add a note callout, like the ones shown in this document, use the ``.. note::`` directive.

.. code-block:: rst

  .. note:: This is a note.

This results in:

.. note:: This is a note.

Additional Reading
------------------

- `asp net style guide <https://docs.asp.net/en/latest/contribute/style-guide.html#style-guide>`_
- `Sphinx documentation <http://sphinx-doc.org/contents.html>`_
- `RST Quick Reference <http://docutils.sourceforge.net/docs/user/rst/quickref.html>`_