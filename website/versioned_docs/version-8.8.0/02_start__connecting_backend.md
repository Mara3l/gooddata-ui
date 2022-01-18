---
title: Set Up an Analytical Backend
sidebar_label: Set Up an Analytical Backend
copyright: (C) 2007-2018 GoodData Corporation
id: version-8.8.0-analytical_backend_integration
original_id: analytical_backend_integration
---

GoodData.UI visual components render data stored in a workspace that exists on an Analytical Backend.

Your application must initialize the integration with the Analytical Backend, select a workspace to work with and then
use these in the React components.

All components accept the `backend` and `workspace` properties. You can use these explicitly or use the `BackendProvider` and `WorkspaceProvider` React providers.

## Initial setup

The following procedure implements the initial setup using the providers to pass down the configured backend and workspace:

1.  Create and set up an instance of the analytical backend to communicate with the GoodData platform:

    ```javascript
    import bearFactory, { ContextDeferredAuthProvider } from "@gooddata/sdk-backend-bear";

    const backend = bearFactory({ hostname })
                    .withAuthentication(new ContextDeferredAuthProvider());
    ```

    This creates a new instance of the analytical backend to communicate with the GoodData platform (codename `bear`) on
    the provided hostname. You may omit the hostname when connecting to the same origin that serves the application.

    The authentication is deferred fully to your application. The analytical backend expects your application code to take
    care of authentication on the GoodData platform (login/SSO). If the analytical backend finds that the context is not
    authenticated, the GoodDataSdkError with the code UNAUTHORIZED will be sent through the onError callback.

    See [Authentication options](02_start__connecting_backend.md#authentication-options) for more information about the supported authentication options.

2.  Wrap your React application with BackendProvider and WorkspaceProvider:

    ```jsx
    <BackendProvider backend={backend}>
        <WorkspaceProvider workspace="your-workspace-id">
            <YourApplicationTree />
        </WorkspaceProvider>
    </BackendProvider>
    ```

## Authentication options

`@gooddata/sdk-backend-bear` has the following built-in authentication providers:

* `ContextDeferredAuthProvider`
* `FixedLoginAndPasswordAuthProvider`

You can also create a custom provider.

### ContextDeferredAuthProvider

`ContextDeferredAuthProvider` assumes that the session is already authenticated to the GoodData platform (either by a login or by SSO).
This is useful when you embed GoodData.UI elements into your app.

To use SSO, follow the [SSO guide](30_tips__sso.md) and use `ContextDeferredAuthProvider` in your application as shown in [Initial setup](02_start__connecting_backend.md#initial-setup).

### FixedLoginAndPasswordAuthProvider

`FixedLoginAndPasswordAuthProvider` allows you to explicitly specify a username/password combination.
This is useful when you handle the authentication yourself (for example, with a custom login form)
or for testing (so that you can hard-code the credentials or provide them from a build script).

To specify the credentials, pass them to the `FixedLoginAndPasswordAuthProvider` constructor. For example:

```js
import bearFactory, { FixedLoginAndPasswordAuthProvider } from "@gooddata/sdk-backend-bear";

const backend = bearFactory({ hostname })
                .withAuthentication(
                    new FixedLoginAndPasswordAuthProvider("username", "password")
                );
```

### Custom AuthProvider

If neither of the built-in providers fits your needs, you can create your own provider by creating a class derived from `BearAuthProviderBase`.
Check [the source code](https://github.com/gooddata/gooddata-ui-sdk/blob/master/libs/sdk-backend-bear/src/auth.ts) out for more details.
