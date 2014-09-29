## Markdown extension (e.g. md, markdown, mdown).
MEXT = md
## All markdown files in the working directory
SRC = $(wildcard week*/*.$(MEXT))
### Location of reveal.js
RJS = ../../../reveal.js

PDFS=$(SRC:.md=.pdf)
HTML=$(SRC:.md=.html)
all:	$(PDFS) $(HTML)
pdf:	clean $(PDFS)
html:	clean $(HTML)

%.html:	%.md
		@cd $(dir $<); pandoc -t revealjs -i \
			--standalone \
			-V revealjs-url=$(RJS) \
			-V theme=moon -V transition=linear \
			-o index.html $(notdir $<)

%.pdf:	%.md
		@cd $(dir $<); pandoc -t beamer -i -s \
			-V theme:default -V colortheme:beaver \
			-o $(notdir $@) $(notdir $<)

clean:
	rm -f week*/*.pdf week*/*.html
