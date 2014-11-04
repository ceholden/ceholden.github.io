## Markdown extension (e.g. md, markdown, mdown).
MEXT = md
## All markdown files in the working directory
SRC = $(wildcard *.$(MEXT))
### Location of reveal.js
RJS = ../../../reveal.js
RJSTEMPLATE = $(RJS)/revealjs_highlight_template.html

HTML=$(SRC:.md=.html)
all:	$(PDFS) $(HTML)
html:	clean $(HTML)

%.html:	%.md
		pandoc -t revealjs -i \
			--standalone \
			--template=$(RJSTEMPLATE) \
 			--no-highlight -V hlss=zenburn \
			-V revealjs-url=$(RJS) \
			-V theme=simple -V transition=linear \
			-o "$@" "$<"

clean:
	rm -f *.html 
