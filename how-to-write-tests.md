# How To Write Tests

Testing style guide for `rails grade`

## Four-phase test

Use clear, [four-phase tests](https://robots.thoughtbot.com/four-phase-test).

## Tests should be readable in isolation

Students should be able to click "Examine Test" and read and understand a test easily. Therefore, each test should be easily understood in isolation.

Therefore,

### Avoid `before`, `let`

[Let's](https://robots.thoughtbot.com/lets-not#will-our-mystery-guest-please-leave) avoid [mystery guests](https://robots.thoughtbot.com/mystery-guest).

### Use a `describe` block with a target URL and a single descriptive test nested inside

**Bad**

```ruby
context "with input 5" do
  it "works", points: 2, hint: h("params_are_strings") do
    visit "/flexible/square/5"

    expect(page).to have_content(25)
  end
end
```

**Good**

```ruby
describe "/flexible/square/5" do
  it "works with input 5", points: 2, hint: h("params_are_strings") do
    visit "/flexible/square/5"

    expect(page).to have_content(25)
  end
end
```

### Avoid deeply nesting `describe`/`feature`, `context`, `it`/`scenario`

#### Bad

```ruby
feature "Flexible square" do
  describe "/flexible/square/42" do
    it "works with input 5", points: 2, hint: h("params_are_strings") do
      visit "/flexible/square/5"

      expect(page).to have_content(25)
    end
  end

  describe "/flexible/square/42" do
    it "works with input 5", points: 4, hint: h("params_are_strings") do
      visit "/flexible/square/42"

      expect(page).to have_content(1764)
    end
  end
end
```

#### Better

```ruby
describe "/flexible/square/5" do
  it "works with input 5", points: 2, hint: h("params_are_strings") do
    visit "/flexible/square/5"

    expect(page).to have_content(25)
  end

  it "works with input 42", points: 4, hint: h("params_are_strings") do
    visit "/flexible/square/42"

    expect(page).to have_content(1764)
  end
end
```

#### Best

```ruby
describe "/flexible/square/5" do
  it "works with input 5", points: 2, hint: h("params_are_strings") do
    visit "/flexible/square/5"

    expect(page).to have_content(25)
  end
end

describe "/flexible/square/5" do
  it "works with input 42", points: 4, hint: h("params_are_strings") do
    visit "/flexible/square/42"

    expect(page).to have_content(1764)
  end
end
```

This also allows for tailoring copy more instructively to each individual spec, rather than shoehorning it to fit a DRYer structure.

### Test features progressively to break a problem into bite-size steps

Add tests for the presence of hardcoded copy or inputs/labels before testing for behavior. This approach lets students better narrow down what they're missing in their code.

**Bad**

```ruby
describe "/photos/new" do
  it "creates a photo when submitted", points: 3, hint: h("button_type") do
    initial_number_of_photos = Photo.count

    visit "/photos/new"

    click_on "Create Photo"

    final_number_of_photos = Photo.count

    expect(final_number_of_photos).to eq(initial_number_of_photos + 1)
  end
end
```

**Good**

```ruby
describe "/photos/new" do
  it "has a form", points: 1 do
    visit "/photos/new"

    expect(page).to have_css("form", count: 1)
  end
end

describe "/photos/new" do
  it "has a label for 'Caption'", points: 1, hint: h("copy_must_match label_for_input") do
    visit "/photos/new"

    expect(page).to have_css("label", text: "Caption")
  end
end

describe "/photos/new" do
  it "has a label for 'Image URL'", points: 1, hint: h("copy_must_match label_for_input") do
    visit "/photos/new"

    expect(page).to have_css("label", text: "Image URL")
  end
end

describe "/photos/new" do
  it "has two inputs", points: 1, hint: h("label_for_input") do
    visit "/photos/new"

    expect(page).to have_css("input", count: 2)
  end
end

describe "/photos/new" do  it "has a button to 'Create Photo'", points: 1, hint: h("copy_must_match") do
    visit "/photos/new"

    expect(page).to have_css("button", text: "Create Photo")
  end
end

describe "/photos/new" do
  it "creates a photo when submitted", points: 3, hint: h("button_type") do
    initial_number_of_photos = Photo.count

    visit "/photos/new"

    click_on "Create Photo"

    final_number_of_photos = Photo.count

    expect(final_number_of_photos).to eq(initial_number_of_photos + 1)
  end
end
```

## One expectation per test

Try to stick to one expectation per test, except when absolutely necessary \(e.g. to ensure proper setup\).

Ref:

[https://devblast.com/b/ruby-testing-with-rspec-one-expectation-per-test](https://devblast.com/b/ruby-testing-with-rspec-one-expectation-per-test)

## Customized Failure Messages

Use customized failure messages for any `expect`s whose messages are not 100% self-explanatory.

Ref:

[https://relishapp.com/rspec/rspec-expectations/docs/customized-message](https://relishapp.com/rspec/rspec-expectations/docs/customized-message)

## Hints

You can add hints to each spec to give students just-in-time help even when we aren't standing next time them. This is next-level rubber-ducky stuff.

For example,

```ruby
it "captures the user's input in the query string with names", points: 4, hint: h("names_for_inputs") do
  visit "/square_root/new"

  expect(page).to have_css("input[name]", count: 1)
end
```

What's going on above:

* You can provide additional help to the student by optionally including a `hint` with the `it` or `scenario` method. The value should be a string or array of strings.
* Keep hints in I18n so that they don't clutter up the readability of tests, and so that you can easily add the same hint to multiple relevant tests:

  ```text
    # config/locales/en.yml

    en:
      hints:
        names_for_inputs: |
                          Give each `<input>` in your form a unique `name=""` attribute.

                          `name=""` is the crucial, functional attribute of an `<input>` that determines what the user's input gets labeled as in the query string, and therefore what key it gets stored under in the `params` hash, and therefore how you will access it in your next RCAV.

                          `placeholder=""`, etc, are just helpful attributes to use to be user-friendly. `name=""` is the functional one.
  ```

* Store hints under keys under `en.hints`.
* You can use GitHub-flavored Markdown.
* To further reduce clutter, there is a helper method `h()` in `spec_helper.rb` which makes it easy to add multiple hints from I18n:

  ```ruby
    def h(hint_identifiers)
      hint_identifiers.split.map { |identifier| I18n.t("hints.#{identifier}") }
    end
  ```

  So you can just provide a single string with the I18n keys of multiple hints separated by spaces:

  ```ruby
    it "works with 42.42", points: 4, hint: h("label_for_input params_are_strings") do
      visit "/square/new"

      fill_in "Enter a number", with: 42.42

      click_button "Calculate square"

      expect(page).to have_content(1799.4564)
    end
  ```

## Use factories

I go back and forth over factories vs just ActiveRecord objects, since students know exactly what ActiveRecord objects are.

Currently I lean towards using factories since, used right, [they produce minimally valid objects out-of-the-box](https://robots.thoughtbot.com/factories-should-be-the-bare-minimum), and so save so much code.

More important than brevity, however, is that you can then define or re-define only the attributes that are important to the test at hand, thereby drawing attention to them.

I think `create(:photo)` is intuitive enough for students to guess what it means; it's no more magical to them than the rest of the test code \(Capybara methods, etc\) that they aren't being explicitly taught.

## Capybara selectors

* tried `has_content`: too much noise
* tried `has_css` with id: unfamiliar \(we could introduce it\)
* tried attribute selector, e.g. `[data-grade="occurrences"]`; too weird looking
* settled on `expect(page).to have_css(".occurrences", text: 2)` for now since it is very familiar to them, but it feels like class is something that is used for too many other things.

Perhaps teaching `id`, `label`, `for`, and styling with `#` earlier so that we can select with it might be worthwhile.

## When stubbing external requests

Testing external requests is tricky since forcing capybara to wait for a response will have inconsistent results. Therefore, it's best to [stub external requests and control the response in our test suite](https://robots.thoughtbot.com/how-to-stub-external-services-in-tests#create-a-fake-hello-sinatra).

Typically, stubbed requests are added in one of the test helper files \(either `spec/spec_helper.rb` or `spec/rails_helper.rb` \) within an `Rspec.configure` block.

Stubbed request should be as flexible and forgiving as possible. Use regexp to:

* Allow for `http` and `https`
* Allow for mixed case
* Allow for dynamic url segments
* Allow for arbitrary additional query string parameters not specified by us \(for example, access tokens\)

## WIP notes below

[http://stackoverflow.com/questions/11377087/can-i-use-capybara-rspec-to-match-a-range](http://stackoverflow.com/questions/11377087/can-i-use-capybara-rspec-to-match-a-range)

_Stubbed requests: Perhaps we create a method for each stubbed request and then call that method at the beginning of the test. Would that be clearer to the student?_

