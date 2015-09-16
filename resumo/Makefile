DOC:=resumo

all: $(DOC).pdf

$(DOC).pdf: $(DOC).tex logo_on.pdf
	pdflatex $<
	pdflatex $<
	pdflatex $<

wc: $(DOC).pdf
	@ pdftotext $< - | wc -w

clean:
	rm -f *.aux *.log $(DOC).pdf
