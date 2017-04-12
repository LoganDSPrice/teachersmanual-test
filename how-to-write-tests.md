# How To Write Tests

Testing style guide for `rails grade`

http://stackoverflow.com/questions/11377087/can-i-use-capybara-rspec-to-match-a-range

### Capybara selectors

- tried `has_content`: too much noise
- tried `has_css` with id: unfamiliar (we could introduce it)
- tried attribute selector, e.g. `[data-grade="occurrences"]`; too weird looking
- settled on `expect(page).to have_css(".occurrences", text: 2)` for now since it is very familiar to them, but it feels like class is something that is used for too many other things.

Perhaps teaching `id`, `label`, `for`, and styling with `#` earlier so that we can select with it might be worthwhile.

### Hints in I18n

Keep hints in I18n so that they don't clutter up the readability of tests, and so that you can easily add the same hint to multiple relevant tests.

### Avoid before, let

No mystery guests. Tests should be readable in isolation.