# How To Create A Project

 1. Download [this railsrc file](https://raw.githubusercontent.com/firstdraft/appdev_template/master/fd) into the folder within which you plan to generate new Rails projects.
 1. Generate your new projects using the railsrc file:
 
    ```bash
    rails new fun_project --rc=fd
    ```

You can peruse the [railsrc file](https://github.com/firstdraft/appdev_template/blob/master/fd) and the [template](https://github.com/firstdraft/appdev_template/blob/master/template.rb) that it invokes to get a sense of what it is doing.

Primarily, it adds some gems that we want to include in all projects, and it gets the project ready for `rails grade`ing.

If there are other things that we ought to be including in projects out of the box, please create an issue or a PR.