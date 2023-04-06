# Terminology

## Understanding the Passwordless.dev API
The Passwordless API utilizes three types of tokens:
* **ApiKey** ```example:public:6b0861e..``` This is a Public API key, safe and intended to be included client side. It allows the browser to connect to out backend and initiate key negotiations and assertions.
* **ApiSecret** ```example:secret:4fd1992..``` This is a Secret API key and should be well protected. It allows your backend to verify sign-ins and register keys on behalf of your users. (Create an account to get your API keys).
* **Token** ```wWdD02ItIvnCKT...``` This is a ephemeral token (exists only temporarily) and is passed between the client, your backend and the Passwordless API. It encodes the status of an ongoing operation, such as registering a credential or signing in. You can think of it as a session or JSON web token (JWT).


## What is FIDO2?

FIDO2 is the umbrella term for branding of world wide web consortium standards (W3C). FIDO2 consistsn of two standardized comppmemts **WebAuthn** and **CTAP**. Together, these standards operate to create a secure, passwordless experience.

* **WebAuthn** is an API that connects a relying party to an application or login system. In a practical sense, WebAuthn creates an easy connection between the web and an application to allow passwordless authentication to occur.
* **CTAP2** The CTAP2 components allows an external and portable authenticator (security key) to operate with a client platform. FIDO CTAP2 is responsible for the external factor, like a security key, communicating with a website or account via an authenticator.

In order to acheive FIDO2 compliance, the authentication process will incormporate both Webathn and CTAP2 standards.


### Security key
A security key is an effective and popular method of adding two-factor authentication (2FA) to an account. A security key is a USB-like physical device that will store and handle cryptography. Security keys are based on FIDO2 authentication standards. 
See [Yubico](https://www.yubico.com/products/security-key/) to learn more about security keys. 

### Relying party
The relying party (RP) is the server that the browser comnmunicates with. If you are a developer redaing this, your server is the relying party and your domain is the relying party ID. 

### User verification 
A FIDO2 server RP can interact with an authenticator to verify a user. This can be done via PIN code, biometrics, or other 2FA methods that securely verify that the proper person is accessing an account. 

### Platform vs. cross-platform
An authenticator can have two classifications:
* A **platform authenticator** is built-in or part of the client platform (eg, Faceid, TouchID, Windows Hello,).
* A **roaming authenticator** ("cross-platform") is detachable (security keys).

