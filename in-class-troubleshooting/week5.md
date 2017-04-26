# Week 5

## General

- still make sure students don't have spaces between method names and arguments, e.g. `render ('show')`
- make sure students have closed the server for other programs and are working in a fresh terminal window in the correct project folder
- make sure students are creating instance variables above the `render` command in controller actions, otherwise the variables won't display in the view


## Photogram Golden Seven

### Setup
- Windows students who are having trouble with ActiveAdmin, should comment out the create admin users line in `seeds.rb`
- If someone has an unresolvable issue in the `application.html.erb` file, just comment out the stylesheet and javascript tags, and include Bootstrap manually with a cdn link. If there is time, check to see if node is properly installed with `node -v` in command prompt with Ruby and Rails

### Create and Update
- make sure the route placeholder matches the key in the params hash in the create and update actions
