L2H = latex2html
LATEX    = latex
PDFLATEX = pdflatex
DVIPS = dvips
# Main input (w/o extension)
MAIN_FNAME=myth
# Additional files the main input file depends on
ADDDEPS=

IMAGES=

RERUN = "(There were undefined references|Rerun to get (cross-references|the bars) right)"

RERUNBIB = "No file.*\.bbl|Citation.*undefined"

GOALS = $(MAIN_FNAME).dvi $(MAIN_FNAME).pdf
DVIFILES = $(MAIN_FNAME).dvi

COPY = if test -r $*.toc; then cp $*.toc $*.toc.bak; fi
RM = /bin/rm -f

main:           $(DVIFILES)

all:            $(GOALS)

$(MAIN_FNAME).dvi: $(MAIN_FNAME).tex $(ADDDEPS) $(patsubst %.png,%.eps,$(IMAGES))
$(MAIN_FNAME).pdf: $(MAIN_FNAME).tex $(ADDDEPS) $(IMAGES)


%.dvi:          %.tex
		$(COPY);$(LATEX) $<
		egrep -c $(RERUNBIB) $*.log && ($(BIBTEX) $*;$(COPY);$(LATEX) $<) ; true
		egrep $(RERUN) $*.log && ($(COPY);$(LATEX) $<) ; true
		egrep $(RERUN) $*.log && ($(COPY);$(LATEX) $<) ; true
		$(COPY);$(LATEX) $< ; true
		if !(cmp -s $*.toc $*.toc.bak); then $(LATEX) $< ; fi
		$(RM) $*.toc.bak
# Display relevant warnings
		egrep -i "(Reference|Citation).*undefined" $*.log ; true
%.png:  %.dia
	dia -e $@ $<

%.png: %.pic
	pic2plot -T png $< > $@

%.ps: %.pic
	pic2plot -T ps $< > $@

%.eps: %.ps
	ps2eps $<

%.eps:  %.dia
	dia -e $@ $<

%.eps:  %.dot
	dot -Tps $< -o $@

%.pdf:  %.eps
	epstopdf $<

%.eps: %.png
	convert $< $@

%.pdf:          %.tex
		$(COPY);$(PDFLATEX) $<
		egrep -c $(RERUNBIB) $*.log && ($(BIBTEX) $*;$(COPY);$(PDFLATEX) $<) ; true
		egrep $(RERUN) $*.log && ($(COPY);$(PDFLATEX) $<) ; true
		egrep $(RERUN) $*.log && ($(COPY);$(PDFLATEX) $<) ; true
		$(COPY);$(PDFLATEX) $< ; true
		if !(cmp -s $*.toc $*.toc.bak); then $(PDFLATEX) $< ; fi
		$(RM) $*.toc.bak
# Display relevant warnings
		egrep -i "(Reference|Citation).*undefined" $*.log ; true

clean:
		$(RM) -f *.aux *.log *.bbl *.blg *.brf *.cb *.ind *.idx *.ilg  \
		*.inx *.ps *.dvi *.pdf *.toc *.out *.lot *.lof *.eps

