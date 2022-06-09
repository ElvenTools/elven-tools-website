---
layout: "docs"
title: "Dapp React hooks and components"
publicationDate: "2022-04-17"
tags:
  - minter dapp
excerpt: "The Elven Tools Dapp React hooks and components that can be used in different combinations."
ogTitle: "Elven Tools Dapp React hooks and components - Elrond custom NextJS Dapp"
ogDescription: "The Elven Tools Dapp React hooks and components that can be used in different combinations."
ogUrl: "https://www.elven.tools/docs/dapp-react-hooks-and-components.html"
twitterTitle: "Elven Tools Dapp React hooks and components - Elrond custom NextJS Dapp"
twitterDescription: "The Elven Tools Dapp React hooks and components that can be used in different combinations."
twitterUrl: "https://www.elven.tools/docs/dapp-react-hooks-and-components.html"
githubUrl: "https://github.com/juliancwirko/elven-tools-website/edit/main/src/docs/dapp-react-hooks-and-components.md"
---

Below you will find the list of most essential utilities, hooks, and components with examples that are actual code from the Dapp. You can search them in the code to better understand how they work.

There are much more hooks and tools, but most of them are already used in the ones listed below.

The code samples are not ready to copy and paste. Please search them in the code.

#### useElrondNetworkSync()

The hook is responsible for synchronizing the network on each refresh. It should be used in the root component. Here is the `_app.tsx`.

Why not the context wrapper? Because context wrappers with auth state data checks will break Next [ASO](https://nextjs.org/docs/advanced-features/automatic-static-optimization).

This way, you can check the auth state in chosen places. You are not forced to do this constantly for the whole document tree.

```jsx
import { useElrondNetworkSync } from "../hooks/auth/useElrondNetworkSync";

const ElvenToolsDapp = ({ Component, pageProps }: AppProps) => {
  useElrondNetworkSync();
  return (
    <ChakraProvider theme={theme}>
      <Component {...pageProps} />
    </ChakraProvider>
  );
};
```

#### useLogin()

The hook is responsible for providing a common interface for all login methods (web wallet, maiar app, browser extension and Ledger). Under the hood it uses three separate hooks: `useWebWalletLogin`, `useMobileAppLogin`, `useExtensionLogin`.

```jsx
const { login, isLoggedIn, error, walletConnectUri, getHWAccounts } = useLogin();
```

The `login` function is a trigger function and it takes the `LoginMethodEnum` as type argument.

The `useLogin` hook looks like:

```jsx
export const useLogin = (params?: Login) => {
  const {
    login: webLogin,
    isLoggedIn: webIsLoggedIn,
    isLoggingIn: webIsLoggingIn,
    error: webLoginError,
  } = useWebWalletLogin(params);

  const {
    login: mobileLogin,
    isLoggedIn: mobileIsLoggedIn,
    isLoggingIn: mobileIsLoggingIn,
    walletConnectUri,
    error: mobileLoginError,
  } = useMobileAppLogin(params);

  const {
    login: extensionLogin,
    isLoggedIn: extensionIsLoggedIn,
    isLoggingIn: extensionIsLoggingIn,
    error: extensionLoginError,
  } = useExtensionLogin(params);

  const {
    login: ledgerLogin,
    isLoggedIn: ledgerIsLoggedIn,
    isLoggingIn: ledgerIsLoggingIn,
    error: ledgerLoginError,
    getHWAccounts,
  } = useLedgerLogin(params);

  const login = async (type: LoginMethodsEnum) => {
    if (type === LoginMethodsEnum.extension) {
      await extensionLogin();
    }
    if (type === LoginMethodsEnum.wallet) {
      await webLogin();
    }
    if (type === LoginMethodsEnum.walletconnect) {
      await mobileLogin();
    }
    if (type === LoginMethodsEnum.ledger) {
      await ledgerLogin(ledgerAccountIndex);
    }
    return null;
  };

  return {
    walletConnectUri,
    getHWAccounts,
    login,
    isLoggedIn:
      webIsLoggedIn ||
      mobileIsLoggedIn ||
      extensionIsLoggedIn ||
      ledgerIsLoggedIn,
    isLoggingIn:
      webIsLoggingIn ||
      mobileIsLoggingIn ||
      extensionIsLoggingIn ||
      ledgerIsLoggingIn,
    error:
      webLoginError ||
      mobileLoginError ||
      extensionLoginError ||
      ledgerLoginError,
  };
};
```

#### LoginModalButton

The component provides the `Connect` button with the modal, which will contain another four buttons for three different authentication possibilities (Maiar Mobile App, Maiar Defi Wallet - browser extension, Elrond Web Wallet, Ledger). You should be able to use it in any place on the website. It also includes the `LoginComponent` (login buttons).

```jsx
import { LoginModalButton } from "../tools/LoginModalButton";

<LoginModalButton />;
```

#### Authenticated

The component is used as a small wrapper where we need to be in the authenticated context, for example, for all transactions.

It can display the spinner and also the fallback React element.

**Important** Do not wrap it in big sections of the code. Its purpose is to be used multiple times on as small blocks as possible.

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

#### useScTransaction()

The hook provides all that is required for triggering smart contract transactions. useScTransaction can also take a callback function as an argument.

```jsx
const { pending, triggerTx, transaction, error } = useScTransaction({ cb });

const mint = async (tokensAmount: number) => {
  const tokens = tokensAmount || 1;
  const totalPayment = new BigNumber(tokenSellingPrice).times(tokens);
  triggerTx({
    func: new ContractFunction(mintFunctionName),
    gasLimit:
      mintTxBaseGasLimit + (mintTxBaseGasLimit / 1.4) * (tokensAmount - 1),
    args: [new U32Value(tokens)],
    value: TokenPayment.egldFromBigInteger(totalPayment),
  });
};
```

#### useScQuery()

The hook uses useSWR under the hood and can be triggered on a component mount or remotely on some action. It has two different states for the pending action. For initial load and on revalidate. It also takes one of two return data types: 'int' and 'string'. You can still use the string type for boolean and check if you will get `01`, which is `true`. For now, it assumes that you know what data type will be returned by a smart contract.

```jsx
const {
  data: queryResult,
  fetch, // you can always trigger the query manually if 'autoInit' is set to false
  isLoading, // pending state for initial load
  isValidating, // pending state for each revalidation of the data, for example using the mutate
  error,
} = useScQuery({
  type: SCQueryType.INT, // can be int or string
  payload: {
    scAddress: mintSmartContractAddress,
    funcName: queryFunctionName,
    args: [],
  },
  autoInit: false, // you can enable or disable the trigger of the query on the component mount
});
```

#### useLoggingIn()

The hook will provide information about the authentication flow state. It will tell if the user is already logged in or is logging in.

```jsx
const { isLoggingIn, error, isLoggedIn } = useLoggingIn();
```

#### useAccount()

The hook will provide information about the user's account data state. The data: address, nonce, balance.

```jsx
const { address, nonce, balance } = useAccount();
```

#### useLoginInfo()

The hook will provide the information about the user's auth data state. The data: loginMethod, expires, loginToken, signature. Login token and signature won't always be there. It depends if you'll use the token. Check [Elven Tools Dapp backend integration article](/docs/dapp-backend-integration.html) for more info.

```jsx
const { loginMethod, expires, loginToken, signature } = useLoginInfo();
```

