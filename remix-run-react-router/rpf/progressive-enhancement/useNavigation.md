
This hook provides information about a pending page navigation.

```ts
import { useNavigation } from "react-router-dom";

function SomeComponent() {
  const navigation = useNavigation();
  // ...
}
```

Copy code to clipboard

## [](https://remix.run/docs/en/main/hooks/use-navigation#properties)Properties

### [](https://remix.run/docs/en/main/hooks/use-navigation#navigationformaction)`navigation.formAction`

The action of the form that was submitted, if any.

```ts
// set from either one of these
<Form action="/some/where" />;
submit(formData, { action: "/some/where" });
```

Copy code to clipboard

### [](https://remix.run/docs/en/main/hooks/use-navigation#navigationformmethod)`navigation.formMethod`

The method of the form that was submitted, if any.

```ts
// set from either one of these
<Form method="get" />;
submit(formData, { method: "get" });
```

Copy code to clipboard

### [](https://remix.run/docs/en/main/hooks/use-navigation#navigationformdata)`navigation.formData`

Any POST, PUT, PATCH, or DELETE navigation that started from a `<Form>` or `useSubmit` will have your form's submission data attached to it. This is primarily useful to build "Optimistic UI" with the `submission.formData` [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData) object.

For example:

```ts
// This form has the `email` field
<Form method="post" action="/signup">
  <input name="email" />
</Form>;

// So a navigation will have the field's value in `navigation.formData`
// while the navigation is pending.
navigation.formData.get("email");
```

Copy code to clipboard

In the case of a GET form submission, `formData` will be empty and the data will be reflected in `navigation.location.search`.

### [](https://remix.run/docs/en/main/hooks/use-navigation#navigationlocation)`navigation.location`

This tells you what the next location is going to be.

### [](https://remix.run/docs/en/main/hooks/use-navigation#navigationstate)`navigation.state`

- **idle** - There is no navigation pending.
- **submitting** - A route action is being called due to a form submission using POST, PUT, PATCH, or DELETE
- **loading** - The loaders for the next routes are being called to render the next page

Normal navigations and GET form submissions transition through these states:

```ts
idle → loading → idle
```

Form submissions with POST, PUT, PATCH, or DELETE transition through these states:

```ts
idle → submitting → loading → idle
```

[Edit](https://github.com/remix-run/remix/edit/main/docs/hooks/use-navigation.md)

