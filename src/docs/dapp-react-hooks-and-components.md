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
const { login, isLoggedIn, error, walletConnectUri, getHWAccounts } = useLogin(params);
```

The `login` function is a trigger function and it takes the `LoginMethodEnum` as type argument.

The `params` for `useLogin` are: `token` and `callbackRoute`, both are optional. You will need to use a custom-generated token to get the auth signature back after connecting with one of 4 auth providers. The callback route can be used for some of the providers to be able to redirect the user after logging in.

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

The component provides the `Connect` button with the modal, which will contain another four buttons for three different authentication possibilities (Maiar Mobile App, Maiar Defi Wallet - browser extension, Web Wallet, Ledger). You should be able to use it in any place on the website. It also includes the `LoginComponent` (login buttons).

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

The hook uses [useSWR](https://swr.vercel.app/) under the hood and can be triggered on a component mount or remotely on some action. It has two different states for the pending action. For initial load and on revalidate. It also takes one of three return data types: 'number', 'string', and 'boolean'. It will implement a result parser based on type definitions in the future.

```jsx
const {
  data: queryResult,
  fetch, // you can always trigger the query manually if 'autoInit' is set to false
  isLoading, // pending state for initial load
  isValidating, // pending state for each revalidation of the data, for example using the mutate
  error,
} = useScQuery<number>({
  type: SCQueryType.NUMBER, // can be number, string or boolean
  payload: {
    scAddress: mintSmartContractAddress,
    funcName: queryFunctionName,
    args: [],
  },
  autoInit: false, // you can enable or disable the trigger of the query on the component mount
});
```

#### useElvenScQuery()

The hook is specific to the Elven Tools Smart Contract and is prepared to query only defined smart contracts. Internally it uses `useScQuery,` and in most cases, you would want to use it instead of the `useScQuery`. At least using the Dapp for Elven Tools Smart Contract interaction.

```jsx
import { SCQueryType } from '../hooks/interaction/useScQuery';
(...)
const {
  data,
  fetch,
  isLoading,
} = useElvenScQuery<boolean>({
  funcName: 'isAllowlistEnabled',
  type: SCQueryType.BOOLEAN,
  autoInit: Boolean(address && !mintingPaused),
});
```

#### useApiCall()

The hook provides a convenient way of doing custom API calls unrelated to transactions or smart contract queries. By default it will use MultiversX API endpoint. But it can be any type of API, not only MultiversX API. In that case you would need to pass the { baseEndpoint: "https://some-api.com" } in options

```jsx
const { data, isLoading, isValidating, fetch, error } = useApiCall<Token[]>({
  url: `/accounts/<some_erd_address_here>/tokens`, // can be any API endpoint without the host, because it is already handled internally
  autoInit: true, // similar to useScQuery
  type: 'get', // can be get, post, delete, put
  payload: {},
  options: {}
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

