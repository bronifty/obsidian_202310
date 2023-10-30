
### Fullstack Data Flow
![](./remix-onewaydataflow.png)
![](./remix-useLoaderData.png)

### Caching
- cache headers and a CDN over ISR

### State Management
1. **Network-related State:** If your React state is managing anything related to the network—such as data from loaders, pending form submissions, or navigational states—it's likely that you're managing state that Remix already manages:
    
    - **[`useNavigation`](https://remix.run/docs/en/main/hooks/use-navigation)**: formData, formAction, formMethod; state, location
    - **[`useFetcher`](https://remix.run/docs/en/main/hooks/use-fetcher)**: formData, formAction, formMethod; state, data
    - **[`useLoaderData`](https://remix.run/docs/en/main/hooks/use-loader-data)**: Access the data for a route. `const {data} = useLoaderData<typeof loader>();`
    - **[`useActionData`](https://remix.run/docs/en/main/hooks/use-action-data)**: errors from the form `const { errors } = useActionData<typeof action>();`

