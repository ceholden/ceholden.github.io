## Markdown extension (e.g. md, markdown, mdown).
MEXT = md
## All markdown files in the working directory
SRC = $(wildcard 201*/*.$(MEXT))
### Location of reveal.js
RJS = ../reveal.js
RJSTEMPLATE = ../template.html

HTML=$(SRC:.md=.html)
all:	$(HTML)
html:	clean $(HTML)

%.html:	%.md
		@cd $(dir $<); pandoc -t revealjs \
			--standalone \
			--template=$(RJSTEMPLATE) \
 			--no-highlight -V hlss=zenburn \
			-V revealjs-url=$(RJS) \
			-V theme=simple -V transition=linear \
			-o index.html $(notdir $<)

clean:
	rm -f 201*/*.html
