---
layout: simple
title: Configure Okta API AM
category: lab
number: 3
---

> In this lab, you configure Okta API AM to protect your Modern App.
> This includes registering and configuring:
> - An OAuth Service Application.
> - An Authorization Server.
> - A custom scope.
> - A custom claim.
> - An access policies with rules.

## Access your Okta Org.
1. Access your Okta org as **okta.admin**.
2. Click **Admin**.
3. Click **Applications**.
4. Click **Register OAuth Service**.
5. Enter **IoT** as Service Name and then click **Save**.
6. Record the **Client ID** and the **Client secret** in a text editor.
    **Tip:** Later, you use these credentials in a IoT solution that will interact in your modern application.

## Register an API AM Authorization Server
> **Notes:**
> - The API AM Authorization Server is a REST API service – located under https://oktaicexxx.oktapreview.com/oauth2/id – that can issue, validate, and revoke OAuth/OIDC tokens.
> - Authorization Servers are the main entry in API AM and from where all API AM features are managed – with exception managing OAuth and OIDC applications.
> - In this lab, you register a new Authorization Server in API AM.
> - This Authorization Server will support custom scopes and claims, as well as access policies for OIDC and Service Applications.

1. Click **Security** > **API**.
2. Click **Add Authorization Server**.
3. Enter the information as follows and then click **Save**.

    | Attribute    | Value                                  |
    |--------------|----------------------------------------|
    | Name         | `API Authorization Server`             |
    | Resource URI | `https://api.oktaice.com`              |
    | Description  | `Protects Okta ICE REST API endpoints` |

    The API Authorization Server page is displayed.
4. Record the Authorization server ID.
    **Note:** The Authorization server ID can be extracted from the Issuer URL: `https://oktaicexxx.oktapreview.com/oauth2/{{authorizationServerId}}`

## Register a Custom Scope

1. In the API Authorization Server page, click **Scopes**.
2. Click **Add Scope**.
3. Enter `promos` as **Name**, `Return discounts and specials for this week` as **Description**, and then click **Create**.
The promos scope is listed in the table.
Tip: Scopes provided by default with OAuth and OIDC – such as openid, or offline_access – cannot be edited or deleted.

## Register a Custom Claim

1. Click Claims.
2. Click Add Claim.
3. Enter the information as follows and then click Create.

    | Attribute  | Value                          |
    |------------|--------------------------------|
    | Name       | `department`                   |
    | Claim type | `Access Token`                 |
    | Value Type | `Expression`                   |
    | Mapping    | `user.department`              |
    | Include in | `The following scopes: promos` |

The department claim is listed in the table.

## Register an Access Policy and Rules

> **Note:** The API AM access policies and rules controls who can request tokens in the Authorization Server. This includes:
> -	What applications can request tokens
> -	What OAuth flows are supported for the token request, and
> -	What scopes, tokens, and claims will be granted by the Authorization Server.
> In this lab, you’ll configure an access policy with rules, so the Authorization Server will issue tokens with custom scopes just for the Service App and the Postman applications.

1. Click Access Policies.
2. Click Add Policy.
3. Enter the information as follows and then click Create Policy.

    | Attribute   | Value                                 |
    |-------------|---------------------------------------|
    | Name        | `Okta Ice Custom Policy`              |
    | Description | `Policy for Okta Ice for custom APIs` |
    | Assign to   | `Postman and Service App`             |

4. Click Add Rule.
5. Enter the information as follows and then click Create Rule.

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


> #### Checkpoint
> At this point you configured Okta API AM to protect your modern application. In the next section, configure your apps to leverage Okta API AM.
