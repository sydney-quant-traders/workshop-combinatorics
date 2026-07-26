.PHONY: all notes clean cleanall watch init

MAIN = main
BUILD_DIR = build

all: init
	latexmk $(MAIN).tex

# Build a speaker-notes PDF (each slide with its \note{} beside it).
# Output: build/main-notes.pdf. Leaves the normal build/main.pdf untouched.
# Run twice so cross-references / overlays settle.
notes: init
	TEXMF_OUTPUT_DIRECTORY="$(CURDIR)/$(BUILD_DIR)" lualatex -interaction=nonstopmode -shell-escape -output-directory=$(BUILD_DIR) -jobname=$(MAIN)-notes "\def\SQTNOTES{}\input{$(MAIN).tex}"
	TEXMF_OUTPUT_DIRECTORY="$(CURDIR)/$(BUILD_DIR)" lualatex -interaction=nonstopmode -shell-escape -output-directory=$(BUILD_DIR) -jobname=$(MAIN)-notes "\def\SQTNOTES{}\input{$(MAIN).tex}"
	@echo "Notes PDF: $(BUILD_DIR)/$(MAIN)-notes.pdf"

watch: init
	latexmk -pvc $(MAIN).tex

clean:
	latexmk -c

cleanall:
	latexmk -C
	rm -rf $(BUILD_DIR)

init:
	@mkdir -p $(BUILD_DIR)