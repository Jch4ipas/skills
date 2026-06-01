---
name: makefile
description: Makefile instructions
license: MIT
compatibility: opencode
---

# Makefile

* Add the `SHELL := /bin/bash` instructions.
* All the `.PHONY:` comes right before the target.
* Regroup all the variables in the beginning of the file.
* Set a default to all variables and ensure there is a way to rewrite them.
* Add a `make help` command that use:  
```sh
.PHONY: help
## Print this help (see <https://gist.github.com/klmr/575726c7e05d8780505a> for explanation)
help:
	@echo "$$(tput bold)Available rules (alphabetical order):$$(tput sgr0)";sed -ne"/^## /{h;s/.*//;:d" -e"H;n;s/^## //;td" -e"s/:.*//;G;s/\\n## /---/;s/\\n/ /g;p;}" ${MAKEFILE_LIST}|LC_ALL='C' sort -f |awk -F --- -v n=$$(tput cols) -v i=20 -v a="$$(tput setaf 6)" -v z="$$(tput sgr0)" '{printf"%s%*s%s ",a,-i,$$1,z;m=split($$2,w," ");l=n-i;for(j=1;j<=m;j++){l-=length(w[j])+1;if(l<= 0){l=n-i-length(w[j])-1;printf"\n%*s ",-i," ";}printf"%s ",w[j];}printf"\n";}'
```
* The `make help` command is the default command.
* Add a `--debug` option that add the `set -e -x` command.
* Always add a `make all` and a `make clean`.
* Add a `make test` command that list all the variables.
* Add some example of usage in a comment at the beginning of the file.
* Add `make up` and `make down` commands (to start and stop the server)
