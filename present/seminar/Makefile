## Markdown extension (e.g. md, markdown, mdown).
MEXT = md
## All markdown files in the working directory
SRC = $(wildcard 201*/*.$(MEXT))
### Location of reveal.js
RJS = ../../../reveal.js
RJSTEMPLATE = ../../default.revealjs.html

HTML=$(SRC:.md=.html)
all:	$(HTML)
html:	clean $(HTML)

%.html:	%.md
		@cd $(dir $<); pandoc -t revealjs -i \
			--standalone \
			--template=$(RJSTEMPLATE) \
			-V width=1600 -V height=900 \
 			-V hlss=zenburn \
			-V revealjs-url=$(RJS) \
			-V theme=simple \
			-V transition=linear \
			-V slideNumber=true \
			-V center=true \
			-V width=1600 -V height=900 \
			-o index.html $(notdir $<)

clean:
	rm -f 201*/*.html
