# work dir
WD := $(shell echo "`pwd`")

DOCKER = docker run --rm -v $(WD):/wd --workdir /wd
CHOWN = chown -R $(shell id -u):$(shell id -g)

.PHONY: generate
generate:
	rm -Rf $(WD)/parser
	mkdir -p $(WD)/parser
	$(DOCKER) any0ne22/antlr4:4.13.0 \
		java \
		-Xmx500M \
		-cp /usr/local/lib/antlr4-tool.jar \
		org.antlr.v4.Tool \
		-o parser \
		-Dlanguage=Go \
		-listener \
		-visitor \
		-package parser \
		WdlV1Parser.g4 \
		WdlV1Lexer.g4
	$(CHOWN) $(WD) || sudo $(CHOWN) $(WD)