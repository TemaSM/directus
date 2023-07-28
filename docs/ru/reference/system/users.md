---
description: REST and GraphQL API documentation on the Users collection in Directus.
readTime: 9 min read
pageClass: page-reference
---

# Users

> Directus Users are the individual accounts that let you authenticate into the API and App. Each user belongs to a Role
> which defines its granular Permissions. [Learn more about Users](/user-guide/overview/glossary#users).

## The User Object

`id` **uuid**\
Primary key of the user.

`first_name` **string**\
First name of the user.

`last_name` **string**\
Last name of the user.

`email` **string**\
Email address of the user.

`password` **hash**\
Password of the user.

`location` **string**\
Location of the user.

`title` **string**\
Title of the user.

`description` **string**\
Description of the user.

`tags` **array**\
Tags for the user.

`avatar` **many-to-one**\
Avatar file. Many-to-one to [files](/reference/files).

`language` **string**\
Language the Admin App is rendered in. See [our Crowdin page](https://locales.directus.io) for all available languages and
translations.

`theme` **string**\
One of `auto`, `light`, `dark`.

`tfa_secret` **string**\
When TFA is enabled, this holds the secret key for it.

`status` **string**\
Status of the user. One of `draft`, `invited`, `active`, `suspended`, `archived`.

`role` **uuid**\
Role of the user. Many-to-one to [roles](/reference/system/roles).

`token` **string**\
Static access token for the user.

`last_access` **date**\
Last time the user accessed the API.

`last_page` **string**\
Last page in the app the user used.

`provider` **string**\
What auth provider was used to register this user.

`external_identifier` **string**\
Primary key of the user in the third party authentication provider, if used.

`auth_data` **json**\
Required data about the user as provided by the third party auth provider, if used.

`email_notifications` **boolean**\
When this is enabled, the user will receive emails for notifications.

```json
{
	"id": "0bc7b36a-9ba9-4ce0-83f0-0a526f354e07",
	"first_name": "Admin",
	"last_name": "User",
	"email": "admin@example.com",
	"password": "**********",
	"location": "New York City",
	"title": "CTO",
	"description": null,
	"tags": null,
	"avatar": null,
	"language": "en-US",
	"theme": "auto",
	"tfa_secret": null,
	"status": "active",
	"role": "653925a9-970e-487a-bfc0-ab6c96affcdc",
	"token": null,
	"last_access": "2021-02-05T10:18:13-05:00",
	"last_page": "/settings/roles/653925a9-970e-487a-bfc0-ab6c96affcdc"
}
```

## List Users

List all users that exist in Directus.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`GET /users`

`SEARCH /users`

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Query {
	users: [directus_users]
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, readUsers } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	readUsers({
		fields: ['*'],
	})
);
```

</template>
</SnippetToggler>

[Learn more about SEARCH ->](/reference/introduction#search-http-method)

#### Query Parameters

Supports all [global query parameters](/reference/query).

### Response

An array of up to [limit](/reference/query#limit) [user objects](#the-user-object). If no items are available, data will
be an empty array.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`GET /users`

`SEARCH /users`

</template>
<template #graphql>

```graphql
query {
	users {
		first_name
		last_name
		email
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, readUsers } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	readUsers({
		fields: ['*'],
	})
);
```

</template>
</SnippetToggler>

## Retrieve a User

List an existing user by primary key.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`GET /users/:id`

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Query {
	users_by_id(id: ID!): directus_users
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, readUser } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	readUser('user_id', {
		fields: ['*'],
	})
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

### Response

Returns the requested [user object](#the-user-object).

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`GET /users/72a1ce24-4748-47de-a05f-ce9af3033727`

</template>
<template #graphql>

`POST /graphql/system`

```graphql
query {
	users_by_id(id: "72a1ce24-4748-47de-a05f-ce9af3033727") {
		first_name
		last_name
		email
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, readUser } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	readUser('0513b6e8-55f2-4ff5-906c-f1a29d7b983c', {
		fields: ['*'],
	})
);
```

</template>
</SnippetToggler>

## Retrieve the Current User

Retrieve the currently authenticated user.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`GET /users/me`

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Query {
	users_me: directus_users
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, readMe } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	readMe({
		fields: ['*'],
	})
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

### Response

Returns the [user object](#the-user-object) for the currently authenticated user.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`GET /users/me`

</template>
<template #graphql>

```graphql
query {
	users_me {
		email
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, readMe } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	readMe({
		fields: ['*'],
	})
);
```

</template>
</SnippetToggler>

## Update the Current User

Update the authenticated user.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`PATCH /users/me`

```json
{
	"user_object_field": "value"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	update_users_me(data: update_directus_users_input!): directus_users
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, updateMe } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	updateMe({
		user_field: 'value',
	})
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

### Response

Returns the updated [user object](#the-user-object) for the authenticated user.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`PATCH /users/me`

```json
{
	"email": "new.email@example.com"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
mutation {
	update_users_me(data: { email: "new.email@example.com" }) {
		email
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, updateMe } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	updateMe({
		email_notifications: false,
	})
);
```

</template>
</SnippetToggler>

## Create a User

Create a new user

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users`

```json
{
	"email": "user_email",
	"password": "user_password",
	"user_object_field": "value"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	create_users_item(data: create_directus_users_input!): directus_users
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, createUser } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	createUser({
		email: 'user_email',
		password: 'user_password',
	})
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

#### Request Body

A partial [user object](#the-user-object).

`email` and `password` are required to authenticate with the default authentication provider.

### Response

Returns the [user object](#the-user-object) for the created user.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users`

```json
{
	"email": "another@example.com",
	"password": "d1r3ctu5",
	"role": "c86c2761-65d3-43c3-897f-6f74ad6a5bd7"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
mutation {
	create_users_item(
		data: {
			email: "another@example.com"
			password: "d1r3ctu5"
			role: { id: "c86c2761-65d3-43c3-897f-6f74ad6a5bd7", name: "Public", admin_access: false, enforce_tfa: false }
		}
	) {
		email
		role
	}
}
```

::: tip

Please note that if you include the Role in the `create_users_items` call it will be treated as an Upsert and not only
as adding a relationship. So make sure the ID exists, and the other parameters match the existing role, otherwise it
could be modified by the user call.

:::

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, createUser } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	createUser({
		email: 'hi@email.com',
		password: 'qwerty123',
	})
);
```

</template>
</SnippetToggler>

## Create Multiple Users

Create multiple new users

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users`

```json
[
	{
		"email": "user_email",
		"password": "user_password",
		"user_object_field": "value"
	},
	{
		"email": "user_email",
		"password": "user_password",
		"user_object_field": "value"
	}
]
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	create_users_items(data: [create_directus_users_input!]!): [directus_users]
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, createUsers } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	createUsers([
		{
			email: 'user_email',
			password: 'user_password',
		},
		{
			email: 'user_email',
			password: 'user_password',
		},
	])
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

#### Request Body

An array of partial [user objects](#the-user-object).

`email` and `password` are required.

### Response

Returns the [user objects](#the-user-object) for the created users.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users`

```json
[
	{
		"email": "admin@example.com",
		"password": "p455w0rd",
		"role": "c86c2761-65d3-43c3-897f-6f74ad6a5bd7"
	},
	{
		"email": "another@example.com",
		"password": "d1r3ctu5",
		"role": "c86c2761-65d3-43c3-897f-6f74ad6a5bd7"
	}
]
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
mutation {
	create_users_items(
		data: [
			{
				email: "admin@example.com"
				password: "p455w0rd"
				role: { id: "c86c2761-65d3-43c3-897f-6f74ad6a5bd7", name: "Public", admin_access: false, enforce_tfa: false }
			}
			{
				email: "another@example.com"
				password: "d1r3ctu5"
				role: { id: "c86c2761-65d3-43c3-897f-6f74ad6a5bd7", name: "Public", admin_access: false, enforce_tfa: false }
			}
		]
	) {
		email
		role
	}
}
```

::: tip

Please note that if you include the Role in the `create_users_items` call it will be treated as an Upsert and not only
as adding a relationship. So make sure the ID exists, and the other parameters match the existing role, otherwise it
could be modified by the user call.

:::

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, createUsers } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	createUsers([
		{
			email: 'hello@email.com',
			password: 'qwerty123',
		},
		{
			email: 'person@email.com',
			password: 'QwErTy1994',
		},
	])
);
```

</template>
</SnippetToggler>

## Update a User

Update an existing user.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`PATCH /users/72a1ce24-4748-47de-a05f-ce9af3033727`

```json
{
	"user_object_field": "value"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	update_users_item(id: ID!, data: update_directus_users_input!): directus_users
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, updateUser } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	updateUser('user_id', {
		user_fiels: 'value',
	})
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

#### Request Body

A partial [user object](#the-user-object).

### Response

Returns the [user object](#the-user-object) for the updated user.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`PATCH /users/72a1ce24-4748-47de-a05f-ce9af3033727`

```json
{
	"title": "CTO"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
mutation {
	update_users_item(id: "72a1ce24-4748-47de-a05f-ce9af3033727", data: { title: "CTO" }) {
		first_name
		last_name
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, updateUser } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	updateUser('e41605bd-f9bc-4c9c-b09d-3ccb7b137fbb', {
		email_notifications: false,
	})
);
```

</template>
</SnippetToggler>

## Update Multiple Users

Update multiple existing users.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`PATCH /users`

```json
{
	"keys": ["user_1_key", "user_2_key"],
	"data": {
		"user_object_field": "value"
	}
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	update_users_items(ids: [ID!]!, data: update_directus_users_input!): [directus_users]
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, updateUsers } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	updateUsers(['user_1_id', 'user_2_id'], {
		user_field: 'value',
	})
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

#### Request Body

`keys` **Required**\
Array of primary keys of the users you'd like to update.

`data` **Required**\
Any of [the user object](#the-user-object)'s properties.

### Response

Returns the [user objects](#the-user-object) for the updated users.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`PATCH /users`

```json
{
	"keys": ["72a1ce24-4748-47de-a05f-ce9af3033727", "9c3d75a8-7a5f-41a4-be0a-1488fd974511"],
	"data": {
		"title": "CTO"
	}
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
mutation {
	update_users_items(
		ids: ["72a1ce24-4748-47de-a05f-ce9af3033727", "9c3d75a8-7a5f-41a4-be0a-1488fd974511"]
		data: { title: "CTO" }
	) {
		first_name
		last_name
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, updateUsers } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	updateUsers(['e41605bd-f9bc-4c9c-b09d-3ccb7b137fbb', '5ec6ee0a-62ad-460d-a91e-fed63e3d804c'], {
		email_notifications: false,
	})
);
```

</template>
</SnippetToggler>

## Delete a User

Delete an existing user.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`DELETE /users/:id`

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	delete_users_item(id: ID!): delete_one
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, deleteUser } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(deleteUser('user_id'));
```

</template>
</SnippetToggler>

### Response

Empty body.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`DELETE /users/72a1ce24-4748-47de-a05f-ce9af3033727`

</template>
<template #graphql>

`POST /graphql/system`

```graphql
mutation {
	delete_users_item(id: "72a1ce24-4748-47de-a05f-ce9af3033727") {
		id
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, deleteUser } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(deleteUser('965749ad-e5e4-4e38-aa91-25a252b8ccd9'));
```

</template>
</SnippetToggler>

## Delete Multiple Users

Delete multiple existing users.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`DELETE /users`

```json
["user_1_key", "user_2_key"]
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	delete_users_items(ids: [ID!]!): delete_many
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, deleteUsers } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(deleteUsers(['user_1_id', 'user_2_id']));
```

</template>
</SnippetToggler>

#### Request Body

An array of user primary keys

### Response

Empty body.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`DELETE /users`

```json
["653925a9-970e-487a-bfc0-ab6c96affcdc", "c86c2761-65d3-43c3-897f-6f74ad6a5bd7"]
```

</template>
<template #graphql>

```graphql
mutation {
	delete_users_items(ids: ["72a1ce24-4748-47de-a05f-ce9af3033727", "9c3d75a8-7a5f-41a4-be0a-1488fd974511"]) {
		ids
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, deleteUsers } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	deleteUsers(['e41605bd-f9bc-4c9c-b09d-3ccb7b137fbb', '5ec6ee0a-62ad-460d-a91e-fed63e3d804c'])
);
```

</template>
</SnippetToggler>

## Invite a new User

Invite a new user by email.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users/invite`

```json
{
	"email": "invited_user_email",
	"role": "invited_user_role"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	users_invite(email: String!, role: String!, invite_url: String): Boolean
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, disableTwoFactor } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(disableTwoFactor('otp'));
```

</template>
</SnippetToggler>

#### Request Body

`email` **Required**\
User email to invite.

`role` **Required**\
Role of the new user.

`invite_url`\
Provide a custom invite url which the link in the email will lead to. The invite token will be passed as a parameter.\
**Note**: You need to configure the
[`USER_INVITE_URL_ALLOW_LIST` environment variable](/self-hosted/config-options#security) to enable this feature.

### Response

Empty body.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users/invite`

```json
{
	"email": "another@example.com",
	"role": "c86c2761-65d3-43c3-897f-6f74ad6a5bd7"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
mutation {
	users_invite(email: "another@example.com", role: "c86c2761-65d3-43c3-897f-6f74ad6a5bd7")
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, inviteUser } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(inviteUser('invited_user_email', 'invited_user_role'));
```

</template>
</SnippetToggler>

## Accept User Invite

Accept your invite. The [invite user endpoint](#invite-a-new-user) sends the email a link to the Admin App.

This link includes a token, which is then used to activate the invited user.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users/invisponse/accept`

```json
{
	"token": "invite_token",
	"password": "user_password"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	users_invite_accept(token: String!, password: String!): Boolean
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, inviteUser } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(inviteUser('another@example.com', 'c86c2761-65d3-43c3-897f-6f74ad6a5bd7'));
```

</template>
</SnippetToggler>

#### Request Body

`token` **Required**\
Accept invite token.

`password` **Required**\
Password for the user.

### Response

Empty body.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users/invite/accept`

```json
{
	"token": "eyJh...KmUk",
	"password": "d1r3ctu5"
}
```

</template>
<template #graphql>

```graphql
mutation {
	users_invite_accept(token: "eyJh...KmUk", password: "d1r3ctu5")
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, acceptUserInvite } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(acceptUserInvite('invite_token', 'user_password'));
```

</template>
</SnippetToggler>

## Generate Two-Factor Authentication Secret

Generates a secret and returns the URL to be used in an authenticator app.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users/me/tfa/generate`

```json
{
	"password": "user_password"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	users_me_tfa_generate(password: String!): users_me_tfa_generate_data
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, acceptUserInvite } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(acceptUserInvite('eyJh...KmUk', 'd1r3ctu5'));
```

</template>
</SnippetToggler>

#### Request Body

`password` **Required**\
The user's password.

### Response

`secret` **string**\
OTP secret to be saved in the authenticator app.

`otpauth_url` **string**\
`otpauth://` formatted URL. Can be rendered as QR code and used in most authenticator apps.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users/me/tfa/generate`

```json
{
	"password": "d1r3ctu5"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
mutation {
	users_me_tfa_generate(password: "d1r3ctu5") {
		secret
		otpauth_url
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, generateTwoFactorSecret } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(generateTwoFactorSecret('user_password'));
```

</template>
</SnippetToggler>

## Enable Two-Factor Authentication

Adds a TFA secret to the user account.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users/me/tfa/enable`

```json
{
	"otp": "One Time Password",
	"secret": "Two-Factor_Authorization_secret"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	users_me_tfa_enable(otp: String!, secret: String!): Boolean
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, generateTwoFactorSecret } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(generateTwoFactorSecret('d1r3ctu5'));
```

</template>
</SnippetToggler>

#### Request Body

`secret` **Required**\
The TFA secret from tfa/generate.

`otp` **Required**\
OTP generated with the secret, to recheck if the user has a correct TFA setup

### Response

Empty response.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users/me/tfa/enable`

```json
{
	"otp": "123456",
	"secret": "3CtiutsNBmY3szHE"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
mutation {
	users_me_tfa_enable(otp: "123456", secret: "3CtiutsNBmY3szHE")
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, enableTwoFactor } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(enableTwoFactor('secret', 'otp'));
```

</template>
</SnippetToggler>

## Disable Two-Factor Authentication

Disables two-factor authentication by removing the OTP secret from the user.

### Request

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users/me/tfa/disable`

```json
{
	"otp": "One-time password"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
type Mutation {
	users_me_tfa_disable(otp: String!): Boolean
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, enableTwoFactor } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(enableTwoFactor('3CtiutsNBmY3szHE', '123456'));
```

</template>
</SnippetToggler>

#### Request Body

`otp` **Required**\
One-time password generated by the authenticator app.

### Response

Empty response.

### Example

<SnippetToggler :choices="['REST', 'GraphQL', 'SDK']" label="API">
<template #rest>

`POST /users/me/tfa/disable`

```json
{
	"otp": "859014"
}
```

</template>
<template #graphql>

`POST /graphql/system`

```graphql
mutation {
	users_me_tfa_disable(otp: "591763")
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, disableTwoFactor } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(disableTwoFactor('591763'));
```

</template>
</SnippetToggler>