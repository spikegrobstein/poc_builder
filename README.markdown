# POC Builder

## About

POC Builder is a project that I created that I use for creating proof of concept applications. Very often, when experimenting with new libraries, APIs, functions and languages, I create a separate, smaller example script to experiment with to get a feel for how it works.

When creating a new project, POC Builder will create a project in the preset directory (`POC_DIR` variable) and turn it into a git repository.

POC Builder is written by Spike Grobstein (spikegrobstein@mac.com ; http://spike.grobste.in) and licensed under the MIT License. You can use and modify it to your hearts content.

## Usage

    poc <action> <project_name> [ <params> ... ]
    
Available actions:

 * `create`: creates a new POC project and initializes as a new git repository. params are files that are to be created in that directory; they will be added to the git repo and committed as part of the initial import.
 * `mate`: open the specified project in textmate. params are ignored.
 * `go`: cd to the specified project directory. params are ignored.
 * `list`: list all available POC projects in the projects directory. params are passed as options to the `ls` command.
 
POC Builder will attempt to `cd` into the project's directory when working with a project (`create`, `mate`, `go`). Because of limitations of the BASH shell, a sub-process cannot change the working directory of its parent process. To work around this, you can "source" the `poc` script by doing the following in an active shell session:

    . path/to/poc create some_project
    
Since always typing the dot and full path can be a pain, you can alias it in your `.bashrc` file:

    alias poc=". path/to/poc"
    
and then you can call `poc` directly from the commandline.

The following environment variables will affect behavior of POC Builder

 * `POC_DIR`: the directory for your POCs
 
## Examples

### Get a list of all POC Projects

    poc list
    
This will list all projects using your default `ls` options

    poc list -Rl
    
This will list all POC projects and their contents in list form
    
### Create a new POC Project

    poc create python_open_file
    
This will create a new project directory called `python_open_file` and initialize a fresh git repository.

    poc create python_open_file open_file.py README
    
This will create a new project directory called `python_open_file`, create 2 empty files called `open_file.py` and `README`, create a fresh git repository, add those files to the repository and commit

### Go to an existing project

    poc go python_open_file
    
This will cd into an existing project directory

### Open a project in textmate

    poc mate python_open_file
    
This will open the existing POC project `python_open_file` in textmate.
