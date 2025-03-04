## chat-e2ee

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/muke1908/chat-e2ee) [![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

The project is still in **development** phase.   


Working prototype:   https://chat-e2ee-2.azurewebsites.net/

---

**Disposable chat session**: this app will allow two mutually agreed users to have a chat in _end-to-end_ encrypted environment. The app itself doesn't track you or ask any infromation from you. Data is owned by **only you** and **only while chatting**. Your private key is generated on your device and never leaves your device. This is not a replacement of your usual chat application.

## Features

1. No login/signp - the end users **don't identify** themselves .
2. Data is **not** stored on any remote server, encrypted data is just relayed to other users, the data can't be decrypted by any man in the middle.  
3. ~~Secure image sharing - 
   **IMPORTANT:** The image sharing feature is imcomplete!! Images are stored to [imagebb](https://mukesh-biswas.imgbb.com/) server. (27/08/2020)~~
4. **No history** i.e. once chat is closed the data is not recoverable, however encrypted data can be found on memory trace. [Read More](https://github.com/muke1908/chat-e2ee/wiki/How-and-when-your-data-can-be-compromised%3F)  

---

**Contribute:**

- [Frontend issues](https://github.com/muke1908/chat-e2ee/issues?q=is%3Aissue+is%3Aopen+label%3Afrontend)
- [Backend issues](https://github.com/muke1908/chat-e2ee/issues?q=is%3Aissue+is%3Aopen+label%3ABackend)
- [![Code Smells](https://sonarcloud.io/api/project_badges/measure?project=muke1908_chat-e2ee&metric=code_smells)](https://sonarcloud.io/project/issues?id=muke1908_chat-e2ee&resolved=false&types=CODE_SMELL)  
- [![](https://img.shields.io/github/issues/muke1908/chat-e2ee?style=flat)](https://github.com/muke1908/chat-e2ee/issues)

For installation instruction, go to [developer section](https://github.com/muke1908/chat-e2ee#for-developers).  

### How to initiate chat

1. Generate unique link.
2. Share the link or PIN with the person you want to chat with.
3. Start chatting.
4. The messages are end-to-end encrypted hence, no one can decrypt your message other than you.

**How the encryption works**

1. Alice and Bob generate a public and private key pair.
2. Alice and Bob share their public keys with each other.
3. Alice encrypts her message with her private key and Bob's public key and sends it to Bob.
4. Bob receives the encrypted message and decrypts it with his private key and Alice's public key.

In this way, no one else can decrypt the message because your private key is never exposed to the internet.
More detailed explanation: https://www.youtube.com/watch?v=GSIDS_lvRv4&t=1s

> We are using NaCL & [TweetNaCL.js](https://github.com/dchest/tweetnacl-js/) library for asymmetric encryption. The NaCL project is being lead by [Daniel J.Bernstein](http://cr.yp.to/djb.html), one of the most prominent Computer Scientists of our era.

---

### Flow

![flow](https://i.imgur.com/2GrBQMz.jpg)

---

### For developers
![Open Source Love](https://img.shields.io/badge/Open%20Source-with%20love-CRIMSON.svg) ![GitHub last commit](https://img.shields.io/github/last-commit/muke1908/chat-e2ee) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=muke1908_chat-e2ee&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=muke1908_chat-e2ee) [![Gitter](https://badges.gitter.im/chat-e2ee/community.svg)](https://gitter.im/chat-e2ee/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

FE: This project includes a light weight frontend UI - bootstrapped with [create-react-app](https://reactjs.org/docs/create-a-new-react-app.html). The FE client is located in `./client` folder.  
BE: The backend runs on express/nodejs. In production mode, express server exposes the API endpoints and serve the static frontend from `./client/build`.

### Installation

1. Fork this repository by clicking on the fork button on the top of this page. This will create a copy of this repository in your account.
2. Now clone the forked repository to your machine. 
3. Run `npm install` in root dir i.e. inside cloned repo.
4. Run `npm run dev` to spin up your client/server. This will run your react app in dev mode and server in watch mode by nodemon.

NOTE: by default `create-react-app` runs webpack-dev-server on port `3000`. The server is configured to run on `3001` port. So make sure that these ports are not blocked on your system.

**Important:** Check `.env.sample` to configure your `.env` file.

To start with docker read the [instructions](https://github.com/muke1908/chat-e2ee/tree/master/docker).   
For native build read the [instructions](https://github.com/muke1908/chat-e2ee/tree/master/native).

### Folder structure

- The FE client is located in `./client` which is coupled with the backend
- All the backend controllers goes to `./backend` folder
- Express instance is on `./app.js`
- Entry point is `./index.js`

### APIs
```endpoint: https://chate2ee.fun/api/<path>```

| url                              | method   | payload                         | filename                  | description                                   |
| -------------------------------- | -------- | ------------------------------ | ------------------------- | --------------------------------------------- |
| `/chat-link`                 | `POST`   | `{token}`                      | `/api/index.js`           | to generate unique link to start chat session |
| `/chat-link/status/:channel` | `GET`    |                                | `/api/index.js`           | to check if a channel is valid                |
| `/chat/message`              | `POST`   | `{ channel, sender, message }` | `/api/messaging/index.js` | to send a message to a specific channel       |
| `/chat-link/:channel`        | `DELETE` |                                | `/api/index.js`           | to delete a channel                           |

---

Please follow the convention for commit message.  
https://github.com/conventional-changelog/commitlint/#what-is-commitlint

Example:  
`git commit -m"feat: some relevant message"`

---

## Contributors ✨

 <img src="https://contributors-img.web.app/image?repo=muke1908/chat-e2ee" />

---
**Cryptographic notice**  
This distribution includes cryptographic software. The country in which you currently reside may have restrictions on the import, possession, use, and/or re-export to another country, of encryption software. BEFORE using any encryption software, please check your country's laws, regulations and policies concerning the import, possession, or use, and re-export of encryption software, to see if this is permitted. See http://www.wassenaar.org/ for more information.

The U.S. Government Department of Commerce, Bureau of Industry and Security (BIS), has classified this software as Export Commodity Control Number (ECCN) 5D002.C.1, which includes information security software using or performing cryptographic functions with asymmetric algorithms. The form and manner of this distribution makes it eligible for export under the License Exception ENC Technology Software Unrestricted (TSU) exception (see the BIS Export Administration Regulations, Section 740.13) for both object code and source code.
