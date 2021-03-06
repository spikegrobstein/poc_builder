# POC Builder

## About

POC Builder is a project that I created that I use for creating proof of concept applications. Very often, when experimenting with new libraries, APIs, functions and languages, I create a separate, smaller example script to experiment with to get a feel for how it works.

When creating a new project, POC Builder will create a project in the preset directory (`POC_DIR` variable) and turn it into a git repository.

POC Builder is written by Spike Grobstein (spikegrobstein@mac.com ; http://spike.grobste.in) and licensed under the MIT License. You can use and modify it to your hearts content.

## Usage

    poc <action> <project_name> [ <params> ... ]
    
Available actions:

 * `create`: creates a new POC project and initializes as a new git repository. params are files that are to be created in that directory; they will be added to the git repo and committed as part of the initial import.
 * `edit`: open the specified project in POC_EDITOR (defaults to `mate`). params are ignored.
 * `go`: cd to the specified project directory. params are ignored.
 * `list`: list all available POC projects in the projects directory. params are passed as options to the `ls` command.
 
POC Builder will attempt to `cd` into the project's directory when working with a project (`create`, `mate`, `go`). Because of limitations of the BASH shell, a sub-process cannot change the working directory of its parent process. To work around this, you can "source" the `poc` script by doing the following in an active shell session:

    . path/to/poc create some_project
    
The following environment variables will affect behavior of POC Builder

 * `POC_DIR`: the directory for your POCs
 * `POC_EDITOR`: the editor for the edit command
    
Since always typing the dot and full path can be a pain, you can alias it in your `.bashrc` file. This is also a good place to configure its environment variables for custom installs:

    export POC_DIR="~/projects/poc"
    export POC_EDITOR="mate"
    
    alias poc=". path/to/poc"
    
and then you can call `poc` directly from the commandline.
 
## Examples

### Get a list of all POC Projects

This will list all projects using your default `ls` options:

    poc list
    
This will list all POC projects and their contents in list form:

    poc list -Rl
      
### Create a new POC Project

This will create a new project directory called `python_open_file` and initialize a fresh git repository:

    poc create python_open_file

This will create a new project directory called `python_open_file`, create 2 empty files called `open_file.py` and `README`, create a fresh git repository, add those files to the repository and commit:

    poc create python_open_file open_file.py README
    
### Go to an existing project

This will cd into an existing project directory:

    poc go python_open_file
    
### Open a project in textmate

This will open the existing POC project `python_open_file` in `POC_EDITOR`:

    poc edit python_open_file
    