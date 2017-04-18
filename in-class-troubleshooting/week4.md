# Week 4

## General

- If students can't see instance variables in their rendered html:
    - make sure that students set the variables above the `render` method call in an action. Otherwise the page will be rendered before the variables are assigned.
    - make sure they have an `=` in their erb tags
- If students can't start their server, check their routes file to make sure there aren't any weird syntax errors
- In routes, make sure `:action` and `:controller` are spelled correctly, singular without any capitalization


## RPS RCAV

### Setup and Guided Work

- If students with windows machines have issues with their command prompt window hanging, closing and restarting Command Prompt with Ruby and Rails has fixed the issue

### Independent Work

- If students have trouble with if-statements, make sure they use `==` for comparison in the conditional as opposed to `=`


### Questions Asked

- How do you set a single instance variable across multiple actions? (before_action)

## Omnicalc Params

### Setup and Guided Work

- Make sure students close their old server and open a new server in the Omnicalc Params project folder
- Make sure the form action attribute has a `/` at the beginning, otherwise the path will be added on to the current url as opposed to replacing it

### Independent Work

- If students are having problems with the flexible payment route, make sure they're not typing decimals into the address bar, e.g. '/flexible/payments/4.5/10/1000' will create problems while '/flexible/payments/45/10/1000' will be fine
