#
How To Write Tests

Testing style guide for `rails grade`

### Four-phase test

Use clear, [four-phase tests](https://robots.thoughtbot.com/four-phase-test).

### Capybara selectors

* tried `has_content`: too much noise
* tried `has_css` with id: unfamiliar \(we could introduce it\)
* tried attribute selector, e.g. `[data-grade="occurrences"]`; too weird looking
* settled on `expect(page).to have_css(".occurrences", text: 2)` for now since it is very familiar to them, but it feels like class is something that is used for too many other things.

Perhaps teaching `id`, `label`, `for`, and styling with `#` earlier so that we can select with it might be worthwhile.

### Hints

You can add a hint to each spec to give students just-in-time help even when we aren't standing next time them. This is awesome, next-level rubber-ducky stuff.

For example,

```ruby
it "captures the user's input in the query string with names", points: 4, hint: h("names_for_inputs") do
  visit "/square_root/new"

  expect(page).to have_css("input[name]", count: 1)
end
```

What's going on above:

- The `points` metadata is giving a weight to the spec for grading purposes. Default is 0.
- The `hint` metadata is where we can provide help. It accepts a string or array of strings.
- Keep hints in I18n so that they don't clutter up the readability of tests, and so that you can easily add the same hint to multiple relevant tests:

    ```yml
    en:
      hints:
        names_for_inputs: |
                          Give each `<input>` in your form a unique `name=""` attribute.

                          `name=""` is the crucial, functional attribute of an `<input>` that determines what the user's input gets labeled as in the query string, and therefore what key it gets stored under in the `params` hash, and therefore how you will access it in your next RCAV.

                          `placeholder=""`, etc, are just helpful attributes to use to be user-friendly. `name=""` is the functional one.
    ```
    
- Store hints under the keys `en.hints`.
- You can use GitHub-flavored Markdown.
- To further reduce clutter, there is a helper method `h()` in `spec_helper.rb` which makes it easy to add multiple hints from I18n:

    ```ruby
    def h(hint_identifiers)
      hint_identifiers.split.map { |identifier| I18n.t("hints.#{identifier}") }
    end
    ```
    
### Avoid before, let

[Let's](https://robots.thoughtbot.com/lets-not#will-our-mystery-guest-please-leave) avoid [mystery guests](https://robots.thoughtbot.com/mystery-guest). Tests should be readable in isolation.

### Use factories

I go back and forth over factories vs just ActiveRecord objects, since students know exactly what ActiveRecord objects are.

Currently I lean towards using factories since, used right, [they produce minimally valid objects out-of-the-box](https://robots.thoughtbot.com/factories-should-be-the-bare-minimum), and so save so much code.

More important than brevity, however, is that you can then define or re-define only the attributes that are important to the test at hand, thereby drawing attention to them.

I think `create(:photo)` is intuitive enough for students to guess what it means; it's no more magical to them than the rest of the test code \(Capybara methods, etc\) that they aren't being explicitly taught.

### When stubbing external requests

Testing external requests is tricky since forcing capybara to wait for a response will have inconsistent results. Therefore, it's best to [stub external requests and control the response in our test suite](https://robots.thoughtbot.com/how-to-stub-external-services-in-tests#create-a-fake-hello-sinatra).

Typically, stubbed requests are added in one of the test helper files \(either `spec/spec_helper.rb` or `spec/rails_helper.rb` \) within an `Rspec.configure` block.

Stubbed request should be as flexible and forgiving as possible. Use regexp to:

* Allow for `http` and `https`
* Allow for mixed case
* Allow for dynamic url segments
* Allow for arbitrary additional query string parameters not specified by us \(for example, access tokens\)

### WIP notes below

[http://stackoverflow.com/questions/11377087/can-i-use-capybara-rspec-to-match-a-range](http://stackoverflow.com/questions/11377087/can-i-use-capybara-rspec-to-match-a-range)

_Stubbed requests: Perhaps we create a method for each stubbed request and then call that method at the beginning of the test. Would that be clearer to the student?_
