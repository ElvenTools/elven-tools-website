---
layout: "docs"
title: "Dapp React hooks and components"
publicationDate: "2022-04-17"
tags:
  - minter dapp
excerpt: "The Elven Tools Dapp React hooks and components that can be used in different combinations."
ogTitle: "Elven Tools Dapp React hooks and components - MultiversX custom NextJS Dapp"
ogDescription: "The Elven Tools Dapp React hooks and components that can be used in different combinations."
ogUrl: "https://www.elven.tools/docs/dapp-react-hooks-and-components.html"
twitterTitle: "Elven Tools Dapp React hooks and components - MultiversX custom NextJS Dapp"
twitterDescription: "The Elven Tools Dapp React hooks and components that can be used in different combinations."
twitterUrl: "https://www.elven.tools/docs/dapp-react-hooks-and-components.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/dapp-react-hooks-and-components.md"
---

Below you will find the list of most essential utilities, hooks, and components with examples that are actual code from the Dapp. You can search them in the code to better understand how they work.

There are much more hooks and tools, but most of them are already used in the ones listed below.

The code samples are not ready to copy and paste. Please search them in the code.

### @useelven/hooks

The template is based on `@useelven/core` npm library.

- [@useelven/hooks docs](https://www.useElven.com) - React hooks for MultiversX blockchain

Besides that, there are custom React components that will help you with development.

#### LoginModalButton

The component provides the `Connect` button with the modal, which will contain another four buttons for three different authentication possibilities (xPortal Mobile App, MultiversX Defi Wallet - browser extension, Web Wallet, Ledger). You should be able to use it in any place on the website. It also includes the `LoginComponent` (login buttons).

```jsx
import { LoginModalButton } from "../tools/LoginModalButton";

<LoginModalButton />;
```

#### Authenticated

The component is used as a small wrapper where we need to be in the authenticated context, for example, for all transactions.

It can display the spinner and also the fallback React element.

**Important** Do not wrap it in big sections of the code. Its purpose is to be used multiple times on as small blocks as possible.

But all code 'blocks' in your app that require the network and auth sync should be wrapped with it.

```jsx
<Authenticated
  spinnerCentered
  fallback={
    <>
      <Text fontWeight="bold" fontSize="2xl" textAlign="center" mt={8}>
        Connect your wallet!
      </Text>
      <Flex mt={4} justifyContent="center">
        <LoginModalButton />
      </Flex>
    </>
  }
>
  <Box>Do something here in the auth context...</Box>
</Authenticated>
```

#### ProtectedPageWrapper

The wrapper component that checks if users are logged in and redirects to chosen path if they are not. You should wrap whole page content with it. You should use it only for pages that should be accessible for logged in users. Remember that this is only client side check.

```jsx
const Profile = () => {
  return (
    <ProtectedPageWrapper>
      <MainLayout>
        <HeaderMenu>
          <HeaderMenuButtons enabled={['auth', 'about', 'mint']} />
        </HeaderMenu>
        <ProfileUserData />
        <ProfileNFTsList />
      </MainLayout>
    </ProtectedPageWrapper>
  );
};
```
#### Check for more

- [Elven Tools Dapp React hooks](https://github.com/ElvenTools/elven-tools-dapp/tree/main/components)
