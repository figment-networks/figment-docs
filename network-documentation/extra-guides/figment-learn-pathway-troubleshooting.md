---
description: Got errors? We've got solutions!
---

# Figment Learn Pathway Troubleshooting

Here are some potential errors you may encounter when following the Learn Pathways, and how to fix them:

## NodeJS version related errors

### Any error relating to missing dependencies _after_ running yarn

Ensure you have a sufficient version of NodeJS installed \(v14.17.6 LTS or higher\) and run the command `yarn` again in the root directory of the project. Note that warnings can appear frequently during the dependency installation process, but these warnings _will not effect the functioning of the Next.js application_.

A list of [Yarn error codes](https://yarnpkg.com/advanced/error-codes) is available, although troubleshooting them is beyond the scope of this document.

### /bin/sh: next: command not found

This error is caused by the installed version of NodeJS being too low. Upgrading to a compatible version of NodeJS will solve this. We recommend using `nvm` , the Node version manager : [https://github.com/nvm-sh/nvm\#install--update-script](https://github.com/nvm-sh/nvm#install--update-script) to install the current LTS version of NodeJS \(v14.17.6\).

### error @polkadot/api@4.17.1: The engine "node" is incompatible with this module. Expected version "&gt;=14.0.0". Got "10.19.0"

This error indicates that the installed version of NodeJS is too low. Upgrading to a compatible version of NodeJS will solve this. We recommend using `nvm` , the Node version manager : [https://github.com/nvm-sh/nvm\#install--update-script](https://github.com/nvm-sh/nvm#install--update-script) to install the current LTS version of NodeJS \(v14.17.6\).

## Browser related errors

### The Safari browser is known to have issues with Next.js' Hot Module Reloading feature

Unfortunately, the Safari web browser is not suitably compatible with the Next.js Hot Module Reloading feature. Use of a supported browser such as Chrome or Firefox is strongly recommended.

## Pathway specific errors

### SyntaxError: Unexpected token u in JSON at position 0

This error can occur during the Solana pathway. It means that the pathway steps were partially completed, and the user came back to complete the pathway, but the localstorage value for `secret` is now `undefined`.   
  
The solution is to start the Solana pathway steps from the beginning, and make sure that the value for `secret` generated during the "Create a Keypair" step is defined during the "Deploy a program" step.



###   

