# CYPRESS

- <https://learn.cypress.io/testing-your-first-application/how-to-test-multiple-pages>
- <https://learn.cypress.io/testing-foundations/testing-is-a-mindset>
- <https://learn.cypress.io/cypress-fundamentals/how-to-write-a-test>
- <https://docs.cypress.io/api/table-of-contents>

## Cypress Basics

`${variable}` : to replace with any values

`npx cypress open` : To start Cypress tooling

`describe(() => { it(); })` : Cypress uses `describe` and `it` like `Jest`

`cy.vist(${link})` : Cypress visits a website

`cy.get(${element_name})` : Cypress gets an element on the website

`cy.get(${element_name}).contains(${element_value}` : Cypress gets an element then check the value of that element is matched with the provided value

`It is recommended to write test based on **data-attribute** rather than classes name, id or type of element (h1, p, ... )`

```jsx
// Element with data-attribute
<h1 data-test="hero-heading">TEST</h1>;

// Cypress test lines
cy.getByData("hero-heading").contains("TEST");
```

Need to add these following line into `cypress/support/command.ts` so we can use short-hand syntax instead of using `.get("[data-test=${value}]")`

```jsx
declare namespace Cypress {
  interface Chainable {
    getByData(dataTestAttribute: string): Chainable<JQuery<HTMLElement>>
  }
}

Cypress.Commands.add("getByData", (selector) => {
  return cy.get(`[data-test=${selector}]`)
})
```

Says there are 2 or more elements with the same type like type `p` If we use `cy.get("p")` it will try to get all the p it can get and have them **in a list** from top to bottom, you can access each p element by using `cy.get("p").eq(0).contains(${test_value})`

If the element is a button after `.get()` we can chain `.click()` to trigger clicking button in Cypress

If the element is a form, we can also chain `.type(${value_we_want_to_add_in_the_form})` to add some value to the form in Cypress

To find an element inside another element we can use `cy.get().find(${element_you_wanna_find})`

To access path URL you can use `cy.location("pathname")`

To check if the content is equal to something or not we can use `cy.get().should("equal", ${some_value})`

Testing pattern : Arrange / Act / Assert

Cypress is running in the browser and has access to anything browser has access to

Cypress `then` and `wrap` methods :

```jsx
cy.get("button").then(($btn) => {
  const cls = $btn.attr("class");

  cy.wrap($btn).click().should("not.have.class", cls);
});
```

Cypress Alias `as(${name})`

```jsx
// Reduce code replication
cy.get("table").find("tr").as("rows");

// Access the cy.get() above easily
cy.get("@rows");
```

You can make Cypress wait for certain action by using both `alias` and `wait`

```jsx
cy.request("POST", "/users").as("signup");

cy.wait("@signup");
```

Cypress `its()` helps you to get a property’s value on previous yielded subject.

```jsx
cy.wrap(["Wai Yan", "Yu"]).its(1).should("eq", "Yu"); // true
cy.wrap({ age: 52 }).its("age").should("eq", 52); // true
cy.wait("@publicTransactions")
  .its("response.body.results")
  .invoke("slice", 0, 5);
```

## The Testing Mindset

- Testing is the most important aspect of software development.
- If you want to write good tests, think about ways to break your application and bulletproof it.
- User Journey is one of the most important tests to make sure all parts of an application work well together.
- Manual testing requires time, effort, and is not automated meaning you have to go and do it yourself every single time you want to do it and in this day and age, time is MONEY.
- As your application developes and it has CI/CD, e2e tests integrated into CI/CD is the only way to make sure your application can deploy to production mutiple times a day with best chance of not having bugs.
- E2E tests > Integration tests > Unit tests
  - E2E tests : user journey imitate what an actual user would do on a website
  - Integration tests : tests that test part of the application works well together or not
  - Unit tests: tests that test a single component / logic / module in the app
