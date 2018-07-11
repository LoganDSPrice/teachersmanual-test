# Updating old projects checklist
 
 - Add gem "console_ip_whitelist", github: "firstdraft/console_ip_whitelist" to the development and test groups
 - Add gem "draft_log", github: "firstdraft/draft_log"to the development and test groups
 - Add gem "better_errors"to the development and test groups
 - Replace the out-of-the-box backtrack_silencers.rb with: https://www.jeffcohenonline.com/templates/backtrace-silencers.rb
 - `bundle update`
 - Add default_whitelist.yml to root folder as in https://github.com/firstdraft-projects/catalog/blob/master/whitelist.yml You may need to rename from whitelist.yml
 - Add whitelist.yml to .gitignore
 - Make sure Hash#[] changes to Hash#fetch in existing code
 - Make sure tempaltes are explicity rendered with the folder name, e.g. render("photo_templates/show.html.erb")
 - Make sure tests are all isolated in their own describe block that contains the action path, e.g "/coffee_beans" instead of "coffee beans index"
 - Make sure all tests that have only_path: true get replaced with ignore_query: true
 - Ensure that CSRF is turned off and authentication tokens are removed from all forms
 - Get rid of //= require_tree . in application.js
 - Get rid of //= require_tree . in application.css
 - Make sure project.rake has an updated org name of 'appdev-projects' and that the app name is update from underscores to dashes, e.g. app-name instead of app_name
 - Ensure that old projects have web_git dependencies: https://github.com/appdev-projects/photogram-auth/commit/016dbbc37e8e285d5ff234a95763a6f28b47802b
 - Make sure the Git url in project.rake is updated from original syntax (git@github.com:appdev-projects/photogram-auth.git) to read-only syntax (git://github.com/appdev-projects/photogram-auth.git)
 - Make sure the READMEs don't have students run the app with bin/server, they should click the Run Project button instead