---
layout: simple
title: Configure Okta API AM
category: lab
number: 1
---

# Configure API AM

> In this lab, you configure Okta API AM to protect your Modern Apps.
> This includes:
> ### Register three OAuth Client Applications
> - **ICE Postman:** A manage (add and remove) entries in the Promos API.
> - **ICE Spa App:** provide a page for users to check promos.
> - **ICE Webhook:** query promos for the Conversational API.
>
> ### Configure Okta API AM
> - **ICE API AM**: An Authorization Server that will concentrate your API security.
> - **promos:create**, **promos:read**, and **promos:cancel**: Custom scopes for the promos API.
> - 2 access policies for administrative and client apps. Each policy will have rules to limit what the app can do.
>
> ### Deploy your Apps
> - **ICE Postman**.
> - **ICE Spa**.
> - **ICE Webhook**
> - **API.ai**
>
> ### Test your Apps
> - Register promos in **Postman**.
> - Check promos as a logged user in **ICE Spa**.
> - Check promos via conversational API with your **API webhook**

## Register OAuth Apps in Okta

### Register OAuth Service Apps

1. Access your Okta org as **okta.admin**.
2. Click **Admin**.
3. Click **Applications**.
4. Click **Register OAuth Service**.
5. Enter **ICE Postman** as Service Name and then click **Save**.
6. Record the **Client ID** and the **Client secret** in a text editor.

    **Tip:** Later, you use these credentials to authenticate the Postman app in Okta.
7. Repeat the steps above to register the **ICE Webhook** app. Record the app credentials.

### Register Single Page Application

1. In the Admin Page, click **Add Application**.
2. Click **Create new App**.
3. Select **SPA** as Platform.

    **Tip:** Okta supports different kinds of OAuth application. Each application may operate with a different OAuth flow.
4. Enter **ICE Spa** as Service Name and then click **Next**.
5. Enter `https://ice-promos-name.herokuapp.com` URI, replacing `name` with your first and last name, and then click **Finish**.
6. Record the **Client ID** in a text editor.

### Checkpoint
> At this point you have three Apps registered in Okta with their respective client credentials.
> During runtime, each of these apps will obtain JWT tokens in Okta API AM using OAuth flows.
> In the next section, you configure how Okta will protect and grant API access for these apps.


## Register an API AM Authorization Server

> **Notes:**
> - The API AM Authorization Server is a REST API service – located under `https://<your_okta_org_url>/oauth2/id` – that can grant, validate, and revoke JWT tokens.
> - OAuth Authorization Servers are the main entity in API AM and from where the API security is configured.
> - In this lab, you register a new Authorization Server that will grant scopes for your promos APIs.

1. Click **Security** > **API**.
2. Click **Add Authorization Server**.
3. Enter the information as follows and then click **Save**.

| Attribute    | Value                                                                        |
|--------------|------------------------------------------------------------------------------|
| Name         | `ICE Promos APIs`                                                            |
| Resource URI | `https://ice-api-name.herokuapp.com`. Replace `name` with your complete name |
| Description  | `Protects all the ICE REST API endpoints, including promos`                  |

    The API Authorization Server page is displayed.
4. Record the **Issuer URL** and the **Audience**.

    The Issuer URL will be used by client applications to contact the ICE APIs authorization server.

## Register Custom Scopes

1. In the API Authorization Server page, click **Scopes**.
2. Click **Add Scope**.
3. Enter `promos:create` as **Name**, `Retrieve promos and specials` as **Description**, and then click **Create**.

    The promos scope is listed in the table.
    Tip: Scopes provided by default with OAuth and OIDC – such as openid, or offline_access – cannot be edited or deleted.

4. Repeat the previous steps to register the scopes `promos:read` and `promos:remove`.

## Register an Access Policy and Rules

> **Note:** The API AM access policies and rules controls who can request tokens to access the Promos APIs. This includes:
> -	What applications can request tokens
> -	What OAuth flows are supported for each app, and
> -	What scopes, tokens, and claims each app can request.

1. Click **Access Policies**.
2. Click **Add Policy**.
3. Enter the information as follows and then click **Create Policy**.

    | Attribute   | Value                                       |
    |-------------|---------------------------------------------|
    | Name        | `Admin Apps`                                |
    | Description | `For apps that will manage the promos data` |
    | Assign to   | `ICE Postman`                               |

4. Click **Add Rule**.
5. Enter the information as follows and then click **Create Rule**.

    | Attribute               | Value                             |
    |-------------------------|-----------------------------------|
    | Rule Name               | `App to App Rule`                 |
    | IF Grant type is        | `Select only Client credentials.` |
    | THEN Grant these scopes | `The following scopes: promos`    |

6. Create a second rule with the following attributes:

    | Attribute               | Value                                          |
    |-------------------------|------------------------------------------------|
    | Rule Name               | `User to App Rule`                             |
    | IF Grant type is        | `Select only Authorization Code and Implicit.` |
    | THEN Grant these scopes | `All scopes.`                                  |


### Checkpoint
> At this point you have:
> - Three Apps registered in Okta with their respective client credentials.
> - An Authorization Server registered in Okta. This server will provide access to the promos APIs under `https://ice-api-name.herokuapp.com`.
> In the next section, you deploy your modern apps to consume the promos API securely.

## Deploy the APIs

1. Go to gitub.
2. Click deploy to heroku.
3. Update environment variables.

## Deploy Postman

1. Launch Postman
2. Import environment and collection.
3. Create a promo.
4. Get promo.

## Deploy API.AI

1. Access API.AI
2. Create an Agent
3. Import a zip file
4. Connect the webhook
5. Configure OAuth

## Test

1. In API.AI, enable preview.

2. Go to webpreview and enter or say `Talk to ice`

3. Login at okta.
    A OAuth/OIDC SSO is executed and the user is redirected back to the test interface.

4. Enter or say `Talk to ice` again.

5. After the welcome message, ask `What are the specials?`.
    A OAuth call is performed and the specials are listed.
