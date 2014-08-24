DOC:=resumo

all: $(DOC).pdf

$(DOC).pdf: $(DOC).tex logo_on.pdf
	pdflatex $<
	pdflatex $<
	pdflatex $<

clean:
	rm -f *.aux *.log $(DOC).pdf
