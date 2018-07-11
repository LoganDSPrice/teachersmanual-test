# Updating old projects checklist

 - Add `gem "console_ip_whitelist", github: "firstdraft/console_ip_whitelist"` to the development and test groups
 - Add [default_whitelist.yml](https://github.com/firstdraft-projects/catalog/blob/master/whitelist.yml) to root folder
 - `git rm whitelist.yml` if present
 - Ensure `whitelist.yml` is gitignored


 - Add gem "console_ip_whitelist", github: "firstdraft/console_ip_whitelist" to the development and test groups
 - Add gem "draft_log", github: "firstdraft/draft_log"to the development and test groups
 - Add gem "better_errors"to the development and test groups
 - Add a file [nicer_errors.rb](https://github.com/firstdraft/appdev_template/blob/master/files/nicer_errors.rb) to `config/initializers`
 - Replace the out-of-the-box backtrack_silencers.rb with [this](https://github.com/firstdraft/appdev_template/blob/master/template.rb#L227)
 - `bundle update`

 - Replace `bin/setup` with [this](https://github.com/firstdraft/appdev_template/blob/master/files/setup)
 
 - Make sure the project setup steps in README are [modern](https://github.com/firstdraft/appdev_template/blob/master/files/README.md)

 - Make sure Hash#[] changes to Hash#fetch in existing code
 - Make sure tempaltes are explicity rendered with the folder name, e.g. render("photo_templates/show.html.erb")
 - Make sure tests are all isolated in their own describe block that contains the action path, e.g "/coffee_beans" instead of "coffee beans index"
 - Make sure all tests that have only_path: true get replaced with ignore_query: true
 - Ensure that CSRF is turned off and authentication tokens are removed from all forms
 - Get rid of //= require_tree . in application.js
 - Get rid of *= require_tree . in application.css
 - Make sure project.rake has an updated org name of 'appdev-projects' and that the app name is update from underscores to dashes, e.g. app-name instead of app_name

 - Make sure the Git url in project.rake is updated from original syntax (git@github.com:appdev-projects/photogram-auth.git) to read-only syntax (git://github.com/appdev-projects/photogram-auth.git)
 - Make sure the READMEs don't have students run the app with bin/server, they should click the Run Project button instead
 
 - gitignire `cloud9_plugins.sh`