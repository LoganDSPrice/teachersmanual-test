# Updating old projects checklist

 - Replace `bin/setup` with [this](https://github.com/firstdraft/appdev_template/blob/master/files/setup) and check to see if project requires `dev:prime` data or not
 - Add `gem "console_ip_whitelist", github: "firstdraft/console_ip_whitelist"` to the development and test groups
 - Add [default_whitelist.yml](https://github.com/firstdraft/appdev_template/blob/master/files/default_whitelist.yml) to root folder
 - `git rm whitelist.yml` if present
 - Ensure `whitelist.yml` is gitignored
 - Ensure `cloud9_plugins.sh` is gitignored
 - Ensure `gem "annotate"` is present, if not add to the `Gemfile` and install it with `rails g annotate:install`
 - Ensure `gem 'activeadmin', github: 'activeadmin/activeadmin'` and `gem 'devise', github: 'plataformatec/devise'` are using the RubyGems version instead of the GitHub. (e.g. just `gem 'activeadmin'` instead of `gem 'activeadmin', github: 'activeadmin/activeadmin'`)
 - Add `gem "better_errors"` and `gem "binding_of_caller"` to the development and test groups
 - Add `gem "draft_log", github: "firstdraft/draft_log"` to the development and test groups
 - Ensure that `gem "web_git", github: "firstdraft/web_git"` is included. Start the server and ensure that navigating to `/git` works.
 - Ensure `db:seeds` is doing `AdminUser.create` and not `AdminUser.create!`
 - Ensure all projects are ready to deploy to Heroku:
     ```
     group :production do
       gem "pg"
       gem "rails_12factor"
     end
     ```
 - Add a file [nicer_errors.rb](https://github.com/firstdraft/appdev_template/blob/master/files/nicer_errors.rb) to `config/initializers`
 - Ensure that in `development.rb` the lines starting with `path = Rails.root.join('whitelist.yml')` and ending with `config.action_mailer.default_url_options = { host: "localhost", port: 3000 }` (non-inclusive) is replaced with:
   ```
       path = Rails.root.join("whitelist.yml")
       default_whitelist_path = Rails.root.join("default_whitelist.yml")
       whitelisted_ips = []
       if File.exist?(path)
         whitelisted_ips = YAML.load_file(path)
       end
       if File.exist?(default_whitelist_path)
         whitelisted_ips = whitelisted_ips.concat(YAML.load_file(default_whitelist_path))
       end
       config.web_console.whitelisted_ips = whitelisted_ips
    ```
 - Replace the out-of-the-box backtrack_silencers.rb with [this](https://github.com/firstdraft/appdev_template/blob/aac1a4090a4d612a2efee4db9273e5fb40478140/template.rb#L227)
 - `bundle update`
 - Make sure the project setup steps in README are [modern](https://github.com/firstdraft/appdev_template/blob/master/files/README.md)
 - Make sure the READMEs don't have students run the app with bin/server, they should click the Run Project button instead

 - Make sure Hash#[] changes to Hash#fetch in existing code
 - Make sure templates are explicitly rendered with the folder name, e.g. `render("photo_templates/show.html.erb")`
 - Make sure tests are all isolated in their own describe block that contains the action path, e.g "/coffee_beans" instead of "coffee beans index"
 - Make sure all tests that have only_path: true get replaced with ignore_query: true
 - Ensure that CSRF is turned off in the `application_controller.rb` with `skip_before_action :verify_authenticity_token, raise: false` and authentication tokens are removed from all forms
 - Get rid of `//= require_tree` . in application.js
 - Get rid of `*= require_tree` . in application.css
 - Make sure project.rake looks [like this](https://github.com/firstdraft/appdev_template/blob/master/files/project.rake) and that the app name is update from underscores to dashes, e.g. app-name instead of app_name

 - Make sure the Git url in project.rake is updated from original syntax (git@github.com:appdev-projects/photogram-auth.git) to read-only syntax (git://github.com/appdev-projects/photogram-auth.git)
- Ensure that all targets have a rake task that runs every hour or so to reset the dev:prime data (since students fill it with garbage)

