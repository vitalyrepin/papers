# Main input (w/o extension)
MAIN_FNAME=QmfRus
# Additional files the main input file depends on
ADDDEPS=

GOALS = $(MAIN_FNAME).pdf
DVIFILES = $(MAIN_FNAME).dvi

main:           $(DVIFILES)

all:            $(GOALS)

IMAGES_EPS=nokia.eps qmf-architecture.eps qs.eps
IMAGES_PNG=$(patsubst %.eps,%.png, $(IMAGES_EPS))

$(MAIN_FNAME).dvi: $(MAIN_FNAME).tex $(ADDDEPS) $(IMAGES_EPS)
$(MAIN_FNAME).pdf: $(MAIN_FNAME).tex $(ADDDEPS) $(IMAGES_PNG)

%.dvi:          %.tex
		latexmk $<

%.pdf:          %.tex
		latexmk -pdf $<

%.png:  %.dot
	dot -Tpng -o$@ $<

%.eps:  %.dot
	dot -Teps -o$@ $<

%.png:  %.dia
	dia -e $@ $<

%.eps:  %.dia
	dia -e $@ $<

%.eps:  %.dot
	dot -Tps $< -o $@

%.pdf:  %.eps
	epstopdf $<

%.eps: %.png
	convert $< $@

%.png: %.jpg
	convert $< $@


clean:
	latexmk -c
	rm -f *.nav *.snm
	rm -f qs.png qs.eps qmf-architecture.eps
