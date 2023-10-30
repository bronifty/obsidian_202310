
A hook for interacting with the server outside of navigation.

```ts
import { useFetcher } from "@remix-run/react";

export function SomeComponent() {
  const fetcher = useFetcher();
  // ...
}
```

Copy code to clipboard

## [](https://remix.run/docs/en/main/hooks/use-fetcher#components)Components

### [](https://remix.run/docs/en/main/hooks/use-fetcher#fetcherform)`fetcher.Form`

Just like [`<Form>`](https://remix.run/docs/en/main/components/form) except it doesn't cause a navigation.

```ts
function SomeComponent() {
  const fetcher = useFetcher();
  return (
    <fetcher.Form method="post" action="/some/route">
      <input type="text" />
    </fetcher.Form>
  );
}
```

Copy code to clipboard

## [](https://remix.run/docs/en/main/hooks/use-fetcher#methods)Methods

### [](https://remix.run/docs/en/main/hooks/use-fetcher#fetchersubmitformdata-options)`fetcher.submit(formData, options)`

Submits form data to a route. While multiple nested routes can match a URL, only the leaf route will be called.

The `formData` can be multiple types:

- [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData) - A `FormData` instance.
- [`HTMLFormElement`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement) - A [`<form>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form) DOM element.
- `Object` - An object of key/value pairs that will be converted to a `FormData` instance.

If the method is `GET`, then the route [`loader`](https://remix.run/docs/en/main/route/loader) is being called and with the `formData` serialized to the url as [`URLSearchParams`](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams). If `DELETE`, `PATCH`, `POST`, or `PUT`, then the route [`action`](https://remix.run/docs/en/main/route/action) is being called with `formData` as the body.

```ts
fetcher.submit(event.currentTarget.form, {
  method: "POST",
});

fetcher.submit(
  { serialized: "values" },
  { method: "POST" }
);

fetcher.submit(formData);
```

Copy code to clipboard

## [](https://remix.run/docs/en/main/hooks/use-fetcher#fetcherloadhref)`fetcher.load(href)`

Loads data from a route loader. While multiple nested routes can match a URL, only the leaf route will be called.

```ts
fetcher.load("/some/route");
fetcher.load("/some/route?foo=bar");
```

Copy code to clipboard

## [](https://remix.run/docs/en/main/hooks/use-fetcher#properties)Properties

### [](https://remix.run/docs/en/main/hooks/use-fetcher#fetcherstate)`fetcher.state`

You can know the state of the fetcher with `fetcher.state`. It will be one of:

- **idle** - Nothing is being fetched.
- **submitting** - A form has been submitted. If the method is `GET`, then the route `loader` is being called. If `DELETE`, `PATCH`, `POST`, or `PUT`, then the route `action` is being called.
- **loading** - The loaders for the routes are being reloaded after an `action` submission.

### [](https://remix.run/docs/en/main/hooks/use-fetcher#fetcherdata)`fetcher.data`

The returned response data from your `action` or `loader` is stored here. Once the data is set, it persists on the fetcher even through reloads and resubmissions (like calling `fetcher.load()` again after having already read the data).

### [](https://remix.run/docs/en/main/hooks/use-fetcher#fetcherformdata)`fetcher.formData`

The `FormData` instance that was submitted to the server is stored here. This is useful for optimistic UIs.

### [](https://remix.run/docs/en/main/hooks/use-fetcher#fetcherformaction)`fetcher.formAction`

The URL of the submission.

### [](https://remix.run/docs/en/main/hooks/use-fetcher#fetcherformmethod)`fetcher.formMethod`

The form method of the submission.

## [](https://remix.run/docs/en/main/hooks/use-fetcher#additional-resources)Additional Resources

**Discussions**

- [Form vs. Fetcher](https://remix.run/docs/en/main/discussion/form-vs-fetcher)
- [Network Concurrency Management](https://remix.run/docs/en/main/discussion/concurrency)

**Videos**

- [Concurrent Mutations w/ useFetcher](https://www.youtube.com/watch?v=vTzNpiOk668&list=PLXoynULbYuEDG2wBFSZ66b85EIspy3fy6)
- [Optimistic UI](https://www.youtube.com/watch?v=EdB_nj01C80&list=PLXoynULbYuEDG2wBFSZ66b85EIspy3fy6)

© [Remix Software, Inc.](https://remix.run/)

•

Docs and examples licensed under [MIT](https://opensource.org/licenses/MIT)

[Edit](https://github.com/remix-run/remix/edit/main/docs/hooks/use-fetcher.md)

1:24

2