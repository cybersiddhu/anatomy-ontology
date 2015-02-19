
# This Makefile is for use by the anatomy Release Manager.
#
# requirements: Oort (http://code.google.com/p/owltools/wiki/OortIntro)
#
# To make a release, type 'make release' in this directory

OBO = http://purl.obolibrary.org/obo

initial-build: anatomy.obo
build: anatomy.obo minidiff
release: anatomy.obo diff

# all release files are derived from the editors version.
# we use the default Oort setup (hermit as reasoner)
anatomy.obo: anatomy-edit.owl
	ontology-release-runner $< --allow-overwrite --asserted --simple

# ----------------------------------------
# Imports
# ----------------------------------------
all_imports: imports/go_import.owl imports/pato_import.owl

imports/%_import.owl: anatomy-edit.owl
	owltools $< $(OBO)/$*.owl --add-imports-from-supports --extract-module -s $(OBO)/$*.owl -c --extract-mingraph  --set-ontology-id $(OBO)/go/extensions/$@ -o $@

# ----------------------------------------
# Diffs
# ----------------------------------------

# 
diff: anatomy.obo
	cd diffs && touch anatomy-diff && rm anatomy-*diff* && make

# Minidiff: intra-release differences
minidiff: anatomy.obo
	cd diffs  && touch anatomy-diff && rm anatomy-*diff* && make TGTS='html txt' SRC=../anatomy.obo && mail -s anatomy-diffs RELEASE-MANAGER@FOO.BAR < anatomy-combined-diff.txt

