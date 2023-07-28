---
description: REST documentation on the Translations collection in Directus.
readTime: 3 min read
pageClass: page-reference
---

# Custom Translations

## The Translations Object

`id` **uuid**\
Primary key of the translations

`key` **string**\
The translation key.

`language` **string**\
The language of the translation.

`value` **string**\
The translation value.

```json
{
	"data": {
		"id": "c4346aa4-81a8-4885-b3a8-f647e4f6f769",
		"key": "Test",
		"language": "en-US",
		"value": "Test"
	}
}
```

## List Translations

List all translations that exist in Directus.

### Request

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`GET /translations`

`SEARCH /translations`

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, readTranslations } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	readTranslations({
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

An array of up to [limit](/reference/query#limit) [translation objects](#the-translations-object). If no items are
available, data will be an empty array.

### Example

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`GET /translations`

`SEARCH /translations`

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, readTranslations } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	readTranslations({
		fields: ['*'],
	})
);
```

</template>
</SnippetToggler>

## Retrieve a Translation

List an existing translation by primary key.

### Request

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`GET /translations/:id`

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, readTranslation } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	readTranslation('translation_id', {
		fields: ['*'],
	})
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

### Response

Returns the requested [translation object](#the-translations-object).

### Example

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`GET /translations/2fc325fb-299b-4d20-a9e7-a34349dee8b2`

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, readTranslation } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	readTranslation('7b8c250a-6864-480f-b230-a4035d155123', {
		fields: ['*'],
	})
);
```

</template>
</SnippetToggler>

## Create a Translation

Create a new translation.

### Request

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`POST /translations`

```json
{
	"translation_field_1": "value_1",
	"translation_field_2": "value_2",
	"translation_field_3": "value_3"
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, createTranslation } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	createTranslation({
		translation_field_1: 'value_1',
		translation_field_2: 'value_2',
		translation_field_3: 'value_3',
	})
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

#### Request Body

A partial [translation object](#the-translations-object).

### Response

Returns the [translation object](#the-translations-object) for the created translation.

### Example

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`POST /translations`

```json
{
	"key": "Test",
	"language": "en-US",
	"value": "My Test"
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, createTranslation } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	createTranslation({
		language: 'fr_FR',
		key: 'test',
		value: 'test',
	})
);
```

</template>
</SnippetToggler>

## Create Multiple Translations

Create multiple new translation.

### Request

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`POST /translations`

```json
[
	{
		"translation_1_field_1": "value_1",
		"translation_1_field_2": "value_2",
		"translation_1_field_3": "value_3"
	},
	{
		"translation_2_field_1": "value_4",
		"translation_2_field_2": "value_5",
		"translation_2_field_3": "value_6"
	}
]
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, createTranslations } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	createTranslations([
		{
			translation_1_field_1: 'value_1',
			translation_1_field_2: 'value_2',
			translation_1_field_3: 'value_3',
		},
		{
			translation_2_field_1: 'value_4',
			translation_2_field_2: 'value_5',
			translation_2_field_3: 'value_6',
		},
	])
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

#### Request Body

An array of partial [translation object](#the-translations-object).

### Response

Returns the [translation object](#the-translations-object) for the created translation.

### Example

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`POST /translations`

```json
[
	{
		"key": "translation.key",
		"language": "en-US",
		"value": "My Translation"
	},
	{
		"key": "translation.key",
		"language": "en-GB",
		"value": "Another Translation"
	}
]
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, createTranslations } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	createTranslations([
		{
			language: 'fr-FR',
			key: 'test',
			value: 'test',
		},
		{
			language: 'it-IT',
			key: 'test_2',
			value: 'test_2',
		},
	])
);
```

</template>
</SnippetToggler>

## Update a Translation

Update an existing translation.

### Request

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`PATCH /translations/:id`

```json
{
	"translation_object_field": "value_1"
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, updateTranslation } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	updateTranslation('translation_id', {
		translation_field: 'value',
	})
);
```

</template>
</SnippetToggler>

### Query Parameters

Supports all [global query parameters](/reference/query).

### Request Body

A partial [translation object](#the-translations-object).

### Response

Returns the [translation object](#the-translations-object) for the updated translation.

### Example

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`PATCH /translations/2fc325fb-299b-4d20-a9e7-a34349dee8b2`

```json
{
	"value": "My Updated Translations"
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, updateTranslation } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	updateTranslation('74f2aa3e-ad5c-424a-9ace-adab5ecb0fca', {
		value: 'this is the new value',
	})
);
```

</template>
</SnippetToggler>

## Update Multiple Translations

Update multiple existing translations.

### Request

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`PATCH /translations`

```json
{
	"keys": ["translation_1_key", "translation_2_key"],
	"data": {
		"field": "value"
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, updateTranslations } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	updateTranslations(['translation_1_id', 'translation_2_id'], {
		field: 'value',
	})
);
```

</template>
</SnippetToggler>

#### Query Parameters

Supports all [global query parameters](/reference/query).

#### Request Body

`keys` **Required**\
Array of primary keys of the translations you'd like to update.

`data` **Required**\
Any of [translation object](#the-translations-object)'s properties.

### Response

Returns the [translation objects](#the-translations-object) for the updated translations.

### Example

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`PATCH /translations`

```json
{
	"keys": ["3f2facab-7f05-4ee8-a7a3-d8b9c634a1fc", "7259bfa8-3786-45c6-8c08-cc688e7ba229"],
	"data": {
		"value": "Test Value"
	}
}
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, updateTranslations } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	updateTranslations(['91be30ed-4f4e-481f-84be-860e0c25b035', '74f2aa3e-ad5c-424a-9ace-adab5ecb0fcajj'], {
		value: 'this is the new value',
	})
);
```

</template>
</SnippetToggler>

## Delete a Translation

Delete an existing translation.

### Request

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`DELETE /translations/:id`

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, deleteTranslation } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(deleteTranslation('id'));
```

</template>
</SnippetToggler>

### Response

Empty body.

### Example

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`DELETE /translations/12204ee2-2c82-4d9a-b044-2f4842a11dba`

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, deleteTranslation } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(deleteTranslation('91be30ed-4f4e-481f-84be-860e0c25b035'));
```

</template>
</SnippetToggler>

## Delete Multiple Translations

Delete multiple existing translations.

### Request

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`DELETE /translations`

```json
["translation_1_key", "translation_2_key", "translation_3_key"]
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, deleteTranslations } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	deleteTranslations(['translation_1_key', 'translation_2_key', 'translation_3_key'])
);
```

</template>
</SnippetToggler>

#### Request Body

An array of translations primary keys

### Response

Empty body.

### Example

<SnippetToggler :choices="['REST', 'SDK']" label="API">
<template #rest>

`DELETE /translations`

```json
["25821236-8c2a-4f89-8fdc-c7d01f35877d", "02b9486e-4273-4fd5-b94b-e18fd923d1ed", "7d62f1e9-a83f-407b-84f8-1c184f014501"]
```

</template>
<template #sdk>

```js
import { createDirectus } from '@directus/sdk';
import { rest, deleteTranslations } from '@directus/sdk/rest';

const client = createDirectus('https://directus.example.com').with(rest());

const result = await client.request(
	deleteTranslations([
		'25821236-8c2a-4f89-8fdc-c7d01f35877d',
		'02b9486e-4273-4fd5-b94b-e18fd923d1ed',
		'7d62f1e9-a83f-407b-84f8-1c184f014501',
	])
);
```

</template>
</SnippetToggler>