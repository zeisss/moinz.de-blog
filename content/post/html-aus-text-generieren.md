+++
date = "2008-11-13T01:31:45+02:00"
title = "HTML aus Text generieren"
lang = "de"
+++

Irgendwie begegnet mir dieses Thema in letzter Zeit immer öfters. Beim Anschauen von [Ewiki](http://github.com/patrikf/ewiki) ist mir [Textile](http://www.textism.com/tools/textile/) und [Markdown](http://daringfireball.net/projects/markdown/) ([PHP](http://michelf.com/projects/php-markdown/)) begegnet: Einfache PHP Klassen, mit der man aus Text entsprechende HTML Seiten generieren kann. Sowas ist ja durchaus nicht nur für Wikis sondern z.B. bei Projekten für das generieren von Dokumentation interessant: Bei [Maven](http://www.maven.org/) wird dieses Prozedere zum generieren der Projektdokumentation genutzt. Da ich aber Maven ansonsten nicht mag, habe ich durchaus einige Zeit damit verbracht ein Standalone-Tool zum generieren solcher Seiten zu suchen. [Docbook](http://www.docbook.org/) mit seinen XML Dateien ist mir irgendwie zu aufgeblasen, wobei ich dies aber nicht wirklich genauer angeschaut habe.

[AsciiDocs](http://www.methods.co.nz/asciidoc/index.html) andererseits bietet zumindest auf den ersten Blick das was ich will:

* Kein aufgeblasenes XML Format
* Die Quelldateien sind auch so gut zu lesen
* Sieht ganz ansehlich aus ohne das man selbst in Stylesheets rumfummeln muss
* Generiert die HTML Dateien mit einem einfachen Aufruf: `asciidoc <file>`
* Schön wäre natürlich noch die generierung eines PDFs, wie Maven dies heute schon kann. Ich werde mal schauen wie weit ich damit komme und dann weiteres davon berichten.

Was mich nur irgendwie stört: Wieso muss jeder sein eigenes Format erfinden? Reicht ein Standardformat mit verschiedenen Extensions nicht aus? Evtl sollte man dafür mal eine RFC schreiben ;)
