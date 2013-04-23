
Thymeleaf Docs
==============

Thymeleaf documentation in Markdown format, which is then converted to both HTML
(using [Pandoc](http://johnmacfarlane.net/pandoc/)) and PDF (using [wkhtmltopdf](http://code.google.com/p/wkhtmltopdf/))
formats using the supplied Gradle build script.


Setup
-----

(I'm going to assume you've got a working Java 6+ environment.)

1. Download and install Gradle: http://www.gradle.org/downloads
2. Download and install Pandoc for your environment: http://johnmacfarlane.net/pandoc/installing.html
   (PDF output is not done using Pandoc, so you don't need to get LaTeX.)
3. Download and install wkhtmltopdf for your environment: http://code.google.com/p/wkhtmltopdf/downloads/list

Optional: If you want to be able to import this project into Eclipse or run the
Gradle job from Eclipse, then install the Groovy-Eclipse and Gradle IDE
components from the [Spring Tool Suite](http://www.springsource.org/sts).


Generating the documentation
----------------------------

Use the Gradle build script to generate the documentation from the Markdown
sources to HTML, PDF, or both.  The following Gradle tasks perform these jobs:

 * `generateDocsHTML` - Create the HTML docs.
 * `generateDocsPDF` - Create the PDF docs (also creates the HTML docs since it
   depends on them)
 * `generateDocs - Creates both HTML and PDF docs (although the PDF task already
   does that... maybe we don't need this task?)

The generated docs will end up in the `build/docs` directory.

Pandoc is used to convert the Markdown sources into HTML, using the `templates/thymeleaf.html`
template.

wkhtmltopdf is used to then create PDF versions of the HTML docs based on the
print stylesheet instead of the screen one you normally see when opening it in
your browser.  This task performs a workaround of launching a Jetty server to
temporarily host the HTML files since wkhtmltopdf uses WebKit, which in turn
prevents many of the JavaScript files in the HTML documentation from running due
to same-origin policies being stricter with the `file://` protocol.

To change the version number that appears in the generated docs, update the
`project.version` property in the `build.gradle` script.
