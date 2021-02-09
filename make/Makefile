# Makefile syntax
# <target_file> : <dependency1> ...
# <TAB> command to produce target file

# If the dependencies or recipe need to take up more than one line, the line
# must be continued using a backslash.

all : espanish.lexc \
	espanish_gen.hfstol \
	espanish_gen.hfstol \
	espanish_ana.png \
	espanish_lexicon.png

espanish.lexc: espanish.lexc

gen.hfst : espanish.lexc
	hfst-lexc <espanish.lexc >espanish_gen.hfst

espanish_gen.hfstol : espanish_gen.hfst
	hfst-fst2fst --optimized-lookup-unweighted -i espanish_gen.hfst -o espanish_gen.hfstol

espanish_ana.hfst : espanish_gen.hfst
	hfst-invert -i espanish_gen.hfst -o espanish_ana.hfst

espanish_ana.hfstol : espanish_ana.hfst
	hfst-fst2fst --optimized-lookup-unweighted -i espanish_ana.hfst -o espanish_ana.hfstol

espanish_ana.png : espanish_ana.hfst
	hfst-fst2txt espanish_ana.hfst | python3 att2dot.py | dot -T png -o espanish_ana.png

espanish_lexicon.png : espanish.lexc
	python3 lexc2dot.py <espanish.lexc | dot -T png -o espanish_lexicon.png  # BUG

.PHONY : clean
clean :
	-rm *.hfst *.hfstol espanish.lexc

.PHONY : test
test :
	sh tests.sh  # sh is a command to run the argument filename as a shell script (usually bash)
