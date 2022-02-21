---
description: Quickstart user guide for DataHub
---

# 🏁 Get Started With DataHub

## 1. Creating an Account

**Step 1:** Users are able to sign up on [**DataHub**](https://datahub.figment.io). When completed, you will receive an invite link such as [https://datahub.figment.io/users/confirm?token=$NumbersAndLetters](https://datahub.figment.io/users/confirm?token=$NumbersAndLetters) to verify your email address.

**Step 2:** Click on this link and you will be redirected to the DataHub dashboard.

## 2. User Dashboard

**Step 1:** Once you have logged in to DataHub, you will need to create a new [app](https://datahub.zendesk.com/hc/en-us/articles/4413167835289-What-are-Apps-) and select the protocol.

![](https://lh3.googleusercontent.com/JRmJgidyYPcK5qqsjW8IsgIk5VsWwsQqsTAeUWC1XwOh2MktnPWMdwW9ZNNswL4Rqlu5kuiDDgWNvy\_jYb7IxXauujoR-Z6WrX2jSFco9VQkPaD\_0lRp5CqJC\_7\_Uhi2LPPSnDme)

**Step 2:** Now, type in the name of your App, select the environment - _Production or Staging_ to differentiate between your apps’ state and select the protocol.

![](https://lh5.googleusercontent.com/jbr3wnHwmKJhdzSYJT4PZrVxwhuTrCliAsgyOax6BeO0Zu8KCKxtLcikzOH\_jLqdTp54vob5AYpmsIrXLvFDIsRjJgPj\_CWsmAN0ljTC0duNs7TWqTox\_i0K-sndGEH34-PE3V-9)

**Step 3:** After creating the app, you will get access to the API key under the “App Overview”, where you can view, copy, create and delete your API keys.

![](https://lh3.googleusercontent.com/2FdhMzg4DJZ3EZJistGRH64RJBJ8FU999sDYTmS40UO2dLLZJ04x58Wf8awd8erv8ekBIEMkx4SiWxMzLVQ1H0rTe72cityeo6LAWvGIXjgeGdoOsVa60ociCmX46\_ZuDCukW9a2)

**Step 4:** Clicking on the “Protocols”, you will be able to see all the services that you are currently subscribed to, and on the same page you can [manage your protocol plan](https://datahub.zendesk.com/hc/en-us/articles/4414935707033-How-do-I-manage-App-or-Protocol-plans-). For ref. in the screenshot below, you can see Solana Mainnet and Devnet RPC.

![](https://lh6.googleusercontent.com/0CldCnmdeMKViQPl7BMMZvGTN92MKzY3t1cQs28reHquuSjjiw2qdK8hTJxIKUjz17RMeBcU0cjRileqPiPPLq2ui\_RjL1iw--ULIAb1FqJN8ffvSXg8gqVmGw2-dPXZ29Dvp3KS)

**Step 5:** You can click on the “See Docs” button to get more info regarding the integration.

![](https://lh4.googleusercontent.com/Anrwdiw3MayGHjnNGrPcLiWy3gI3fOfcWG-nul4a3fGAVkpI3L0thnCZshNi4jHwvpZJINTbKD9qcFml95NzYOD4woSiW4r8ybKE7fynqoihM4k6TB-miqqmsg56sYMuFEHaRlPi)

**Step 6:** You can click on the “ANALYTICS” button on the dashboard to get access to your request logs. Read more about the DataHub analytics **** [**HERE**](https://datahub.zendesk.com/hc/en-us/articles/4413198044057-What-App-analytics-does-DataHub-provide-)

**Step 7:** To invite your team members and collaborate with them on the project, click on the “TEAM” button on the dashboard. Read more about App team roles and permissions **** [**HERE**](https://datahub.zendesk.com/hc/en-us/articles/4413168141977-What-are-App-Team-Roles-and-Permissions-)

**Step 8:** To manage the payment method, protocols, check invoices and delete apps, etc. click on “SETTINGS” on the dashboard.

![](https://lh4.googleusercontent.com/sIZziG9XKMVZg44QGok7s8hrWXGBOzQ1TV4z9k3axP8NAXQCUmfL3N2E8CIfgtLINwBquqf3iit10BRJ0wpeHde7P9m-RnUMx-lqgL7VE4N9bMHZ-ShqXaAEFiXtRwmxtJST6Iwi)

## **3.** Accessing a Network

In this example, we’ll access the Solana Devnet -

**Step 1:** When clicking on the “See Docs” button, you will be provided with the URL for this service.

![](https://lh5.googleusercontent.com/fLGGFFfFCnTFYhBi4DkOUpefVjSmpVNhOEr2fEN\_rGjw-\_w3LVTB3BZHKsyMK7rihWjbWmg\_y1Uos2-SXuga1kCfHlECBEEKPniwe8hsfEBa36osOc1lVCCGRyS-omsuYrlogiYt)

**Step 2:** Depending on your setup, there are two ways to use your API key. You can specify your API key with the Authorization header. Here is an example curl:

```
curl https://solana--devnet.datahub.figment.io/health -H "Authorization: YOUR_API_KEY"
```

Or you can specify your API key as a prefix to the path like, `/apikey/YOUR_API_KEY/the`\_`path`. If choosing this option, the full path for curl would look like this:

```
curl https://solana--devnet.datahub.figment.io/apikey/YOUR_API_KEY/health
```

****[**Sign up now**](https://datahub-beta.figment.io/auth/login) to start building in minutes and discover the superpowers Datahub can offer you!

[**Subscribe**](https://datahub.figment.io/subscribe) to the DataHub newsletter to be the first to know about new protocols launches and new features!
