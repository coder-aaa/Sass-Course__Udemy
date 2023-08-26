# -*- MakeFile -*-
#Setting a shell
SHELL := powershell.exe
#Syntax
# % wildcard meaning any
# example %.c meaning any c 
# $@ is replaced with the target
# $^ is replaced with the dependency
#target: dependencies
#	action
BASEDIR = ./css/sass
GENCSS = ./css/style.css
# Gets all the directory in base directory
SASSDIR = $(foreach DIR, $(BASEDIR), $(wildcard $(DIR)/*))
# Get all files that end with scss
SASSFILESPATH = $(foreach DIR, $(SASSDIR), $(wildcard $(DIR)/*.scss))
OutputFile := $(BASEDIR)/main.scss
RELATIVEPATH =  $(foreach FILE, $(SASSFILESPATH), $(subst $(BASEDIR),.,$(FILE)))

all: clean $(OutputFile) fixMain sass

$(OutputFile):
	$(SHELL) [Console]::OutputEncoding = [System.text.Encoding]::UTF8
	$(SHELL) new-item $(OutputFile)
#add imports for each file found in sass directories
	$(SHELL) $(foreach FILE, $(RELATIVEPATH),   Add-Content -Path $(OutputFile) -Value '//'; Add-Content -Path $(OutputFile) -Value '@import "$(FILE)";'; )


sass:  
	sass --watch $(OutputFile):$(GENCSS)

clean:
	rm css/style.*
	rm $(BASEDIR)/main.*



fixMain: 
	$(SHELL) cat $(OutputFile) | foreach($$_){ $$_ -replace "//"} | Set-Content $(OutputFile)
