all:	sachs.png sachs.eps

%.png:  %.dot
	dot -Tpng -o$@ $<

%.eps:  %.dot
	dot -Teps -o$@ $<

clean:
		$(RM) -f *.png *.eps
