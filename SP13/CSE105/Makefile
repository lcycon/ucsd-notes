PDFS := $(patsubst %.md,%.pdf,$(wildcard *.md))

%.pdf: %.md
	pandoc -V geometry:margin=1in -o $@ $*.md

all: $(PDFS)

clean:
	rm -f *.pdf
