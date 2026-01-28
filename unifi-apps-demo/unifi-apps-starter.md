# Unifi Apps Starter

Starting Mini App development can be challenging. The Unifi Apps Starter provides a solid foundation to kickstart your project.

This template includes the essential features needed for building a Mini App, allowing you to customize and build your own application efficiently. This guide covers:

* [What is the Unifi Apps Starter?](unifi-apps-starter.md#what-is-the-unifi-apps-starter)
* [Getting Started](unifi-apps-starter.md#how-to-get-started-with-the-unifi-apps-starter) (Environment setup, Source code, Deployment)
* [Key features](unifi-apps-starter.md#key-features-of-the-unifi-apps-starter) (Wallet connection, Payments, LIFF integration)

## What is the Unifi Apps Starter?

The **Unifi Apps Starter** is a template project designed to help you easily integrate the `dapp-portal-sdk`. While you can always start your Mini App project from scratch, using this starter allows for a faster and smoother development experience.

It also follows a predefined design guide, which can help maintain consistency in UI/UX.

The project is built with **Next.js**. Even if you're planning to use a different framework, this repository can still serve as a useful reference for integrating the `dapp-portal-sdk`.<br>

## How to get started with the Unifi Apps Starter Environment

The Unifi Apps Starter requires **Node.js** to run. It uses `pnpm` as the package manager (compatible with `npm`).

* Recommended Node.js version: **>= 20.0.0**
* The version specified in `.nvmrc`: **v20.18.0**
* Older versions may work partially, but for compatibility with Netlify deployment tools, Node.js >= 20.0.0 is required.

\*Tip: Use [`nvm`](https://github.com/nvm-sh/nvm) to manage Node versions easily.

### Downloading and running the source code&#x20;

You can clone or fork the repository from GitHub:\
[ https://github.com/techreadiness/unifi-apps-starter](https://github.com/techreadiness/unifi-apps-starter)

To run the project locally, follow the instructions in the repository’s `README.md`.

### Deploying to a server

Once you’ve run the Unifi Apps Starter locally and verified that it's working, you can deploy it to a live server using **Netlify**:

<details>

<summary>A netlify account is required </summary>

[Netlify (opens new window)](https://www.netlify.com/)is a hosting service for static sites, open an account before deploying to Netlify. The content on this page can be run on Netlify's free plan.

</details>

```bash
# Go to the root directory
cd ./
# Build the project
pnpm build 
# Deploy to a draft (preview) environment
netlify deploy
# Once verified, deploy to production
netlify deploy --prod 
```

## Key features of the Unifi Apps starter

The Unifi Apps Starter comes with several basic features implemented out of the box.\
These demonstrate how to use core functionalities from `dapp-portal-sdk`, but should be treated as **reference code**, not a final solution.

### Connect/Disconnect wallet

Connecting and disconnecting a wallet is the most fundamental feature when using the SDK.\
In the code, you’ll find how to use `walletProvider` and its methods.

### Crypto/Fiat payment

The template shows how to handle both **crypto** and **fiat** payments using `paymentProvider`.

You can see examples of:

* Creating paymentId
* Checking the payment status
* Finalizing the payment

### KAIA/STRIPE ratio

To support payments, your Mini App needs to apply proper price conversion logic between **crypto (KAIA)** and **fiat (STRIPE)**.\
The starter includes a `usd-to-kaia` function as a reference.

### LIFF integration

If you're planning to integrate with **LINE Front-end Framework (LIFF)**, this project includes useful examples such as:

* When to initialize LIFF
* How to use methods like `shareTargetPicker`
