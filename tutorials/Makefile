BUILD := build
SOURCES := $(filter-out common.tex,$(wildcard *.tex))
$(info SOURCES:$(SOURCES))

TUTORIALS := $(patsubst %.tex,$(BUILD)/%.pdf,$(SOURCES))

all: $(TUTORIALS)

$(BUILD):
	mkdir -p $(BUILD)

$(BUILD)/%.pdf: %.tex common.tex $(BUILD) Makefile
	@echo + Making $@ from $<
	pdflatex -output-directory=$(BUILD) "$(patsubst $(BUILD)/%.pdf,%.tex,$@)"
	bibtex "$(patsubst $(BUILD)/%.pdf,$(BUILD)/%,$@)"
	pdflatex -output-directory=$(BUILD) "$(patsubst $(BUILD)/%.pdf,%.tex,$@)"
	pdflatex -output-directory=$(BUILD) "$(patsubst $(BUILD)/%.pdf,%.tex,$@)"
# 	cp $@ "$(patsubst $(BUILD)/%.pdf,%.pdf,$@)"

$(TUTORIALS) : $(BUILD)/%.pdf : %.tex

# rm -fr $(BUILD)
clean:
	rm -fr *.aux *.log *.out *.pdf *.synctex.gz *.pdfsync
