---
title: Overview
level1: Documents
level2: Consumer Experience
level3: Connector API
order: 1
level-order: 8
root-link: true
indicator: both
permalink: connectorapioverview.html
---

### Connector API

An overview of the Connector API.

### Getting Started

A few things you'll need to get started with this API:

1. **Retrieve your domain**. Use the [LivePerson Domain API](agent-domain-domain-api.html){:target="_blank"} to retrieve this information by providing the following service name:

	* Read only: accountConfigReadOnly

	* Read/Write: accountConfigReadWrite

2. This API requires authorization using the OAuth2.0 methodolgy, via an app key and secret. In order to obtain everything you need to authenticate with OAuth2.0, you will need to install an LE App. Please follow this guide in order to do so.

	* **Log a user into LiveEngage** using the [Login Service API](login-getting-started.html){:target="_blank"}. Provide a username and password, and receive an authorization token (bearer). Use this token as your authorization header in all API requests.

	* [Follow these instructions](guides-gettingstarted.html){:target="_blank"}, to create and use an API key.

3. [Here are the API terms of use](https://www.liveperson.com/policies/terms-of-use){:target="_blank"}.

### Use Cases

Examples of use cases for the API.

### Best Practices
