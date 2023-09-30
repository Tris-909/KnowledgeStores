# Playwright

## Navigation

await page.goto(link)

## Get Elements For Testing

- `await page.getByRole(role, { name: role_cotent })` → Get an element by specifying role ( button, heading, checkbox, … )
- `await page.getByText(text_content)` → Get an element by searching for it’s text content
- `await page.getByLabel(label)` → Get an element form fields using the content inside `<label>content</label>`
- `await page.getByPlaceholder(place_holder)` → Get an element from fields using content inside `placeholder` ( `placeholder` can usually find on `input` element )
- `await page.getByAltText(alt_text)` → Get an image element using it’s content inside `alt` attribute for `<image />` element
- `await page.getByTitle(title)` → Get an element that has `title` attribute
- `await page.getByTestId(test_id)` → Get an element that has `data-testid` attribute

If we get many elements as once, we might want to use .filter({ method_filter : content_filter }) for filtering out the exact element we want ( visit https://playwright.dev/docs/locators#filtering-locators to know more advanced filters ). There are a few method for method_filter like :

- `has`
- `hasNot`
- `hasNotText`
- `hasText`

## Actions

Checkbox → `.check()` `.uncheck()`

Input → `.fill()`

Dropdown → `selectOption()`

FileUpload → `.setInputFiles()`

General Element → `.click()` `.hover()` `.focus()` `.press()`

## Assertions

_Text Assertion :_

`toEqual`

`toContain`

[`.toContainText()`](https://playwright.dev/docs/api/class-locatorassertions#locator-assertions-to-contain-text)

[`.toHaveTitle()`](https://playwright.dev/docs/api/class-pageassertions#page-assertions-to-have-title)

[`.toHaveText()`](https://playwright.dev/docs/api/class-locatorassertions#locator-assertions-to-have-text) : Absolute equal text, have to be the same 100% to pass the test

_Value Assertion :_

`toBeTruthy`

[`.toHaveValue()`](https://playwright.dev/docs/api/class-locatorassertions#locator-assertions-to-have-value)

_Behaviour Assertion :_

[`.toBeVisible()`](https://playwright.dev/docs/api/class-locatorassertions#locator-assertions-to-be-visible)

[`.toBeChecked()`](https://playwright.dev/docs/api/class-locatorassertions#locator-assertions-to-be-checked)

[`.toBeEnabled()`](https://playwright.dev/docs/api/class-locatorassertions#locator-assertions-to-be-enabled)

[`.toHaveAttribute()`](https://playwright.dev/docs/api/class-locatorassertions#locator-assertions-to-have-attribute)

[`.toHaveCount()`](https://playwright.dev/docs/api/class-locatorassertions#locator-assertions-to-have-count)

[`.toHaveURL()`](https://playwright.dev/docs/api/class-pageassertions#page-assertions-to-have-url)
