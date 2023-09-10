# -*- MakeFile -*-
#Setting a shell
SHELL := powershell.exe
#Syntax
# % wildcard meaning any
# example %.c meaning any c
# $@ is replaced with the target
# $^ is replaced with the dependency
# @ does not log the what the action does
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

all: clean minimizeFile sass

$(OutputFile):
	@$(SHELL) [Console]::OutputEncoding = [System.text.Encoding]::UTF8
#imports for each file found in sass directories
	@$(SHELL) Add-Content $(OutputFile) -Value "//"; Add-Content $(OutputFile) -Value "@import" -NoNewLine; $(foreach FILE, $(RELATIVEPATH),\
		Add-Content -Path $(OutputFile) -Value\
		"`"$(FILE)`"," -NoNewLine;)
	@$(SHELL) Add-Content $(OutputFile) -Value "//" -NoNewLine ; Add-Content $(OutputFile) -Value ";" -NoNewLine;


sass:
	@$(SHELL) sass --watch $(OutputFile):$(GENCSS)

clean:
	@$(SHELL) rm css/style.*
	@$(SHELL) rm $(BASEDIR)/main.scss



minimizeFile:$(OutputFile)
	@$(SHELL) cat $^ | foreach($$_){ $$_ -replace ",//"} | Set-Content $^
	@$(SHELL) cat $^ | foreach($$_){ $$_ -replace "//"} | Set-Content $^
	@$(SHELL) cat $^ | foreach($$_){ $$_ -replace "\s"} | Set-Content $^
	@$(SHELL) cat $^ | Where-Object{ $$_ -match "\S"} | Set-Content $^
