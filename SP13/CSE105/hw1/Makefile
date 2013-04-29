PDFS := $(patsubst %.md,%.pdf,$(wildcard *.md))
deps := $(wildcard *.jpg)

%.pdf: %.md $(deps)
	pandoc -V geometry:margin=1in -o $@ $*.md

all: $(PDFS)

clean:
	rm -f *.pdf
