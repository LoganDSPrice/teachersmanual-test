# How To Write Tests

Testing style guide for `rails grade`

### Four-phase test

Use clear, [four-phase tests](https://robots.thoughtbot.com/four-phase-test).

### Capybara selectors

- tried `has_content`: too much noise
- tried `has_css` with id: unfamiliar (we could introduce it)
- tried attribute selector, e.g. `[data-grade="occurrences"]`; too weird looking
- settled on `expect(page).to have_css(".occurrences", text: 2)` for now since it is very familiar to them, but it feels like class is something that is used for too many other things.

Perhaps teaching `id`, `label`, `for`, and styling with `#` earlier so that we can select with it might be worthwhile.

### Hints in I18n

Keep hints in I18n so that they don't clutter up the readability of tests, and so that you can easily add the same hint to multiple relevant tests.

### Avoid before, let

[Let's](https://robots.thoughtbot.com/lets-not#will-our-mystery-guest-please-leave) avoid [mystery guests](https://robots.thoughtbot.com/mystery-guest). Tests should be readable in isolation.

### Use factories

I go back and forth over factories vs just ActiveRecord objects, since students know exactly what ActiveRecord objects are.

Currently I lean towards using factories since, used right, [they produce minimally valid objects out-of-the-box](https://robots.thoughtbot.com/factories-should-be-the-bare-minimum), and so save so much code.

More important than brevity, however, is that you can then define or re-define only the attributes that are important to the test at hand, thereby drawing attention to them.

I think `create(:photo)` is intuitive enough for students to guess what it means; it's no more magical to them than the rest of the test code (Capybara methods, etc) that they aren't being explicitly taught.

### WIP notes below

http://stackoverflow.com/questions/11377087/can-i-use-capybara-rspec-to-match-a-range

