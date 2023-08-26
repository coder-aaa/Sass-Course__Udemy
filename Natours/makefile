# -*- MakeFile -*-
#Setting a shell
SHELL := powershell.exe
#Syntax
#target: dependencies
#	action

all: clean sass

sass: open 
	sass --watch ./css/sass/main.scss:./css/style.css

clean:
	rm css/style.*

open:
	$(SHELL) ii index.html


min:
	$(SHELL) cat index.html | -replace '\s' ''