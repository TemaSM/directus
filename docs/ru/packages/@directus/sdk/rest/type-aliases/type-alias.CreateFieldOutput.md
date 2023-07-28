---
editLink: false
---

# Type alias: CreateFieldOutput`<Schema, TQuery, Item>`

> **CreateFieldOutput**: \<`Schema`, `TQuery`, `Item`\>
> [`ApplyQueryFields`](../../types-1/type-aliases/type-alias.ApplyQueryFields.md)\< `Schema`, `Item`,
> `TQuery`[`"fields"`] \>

## Type parameters

| Parameter                                                                                       | Default                                                                                |
| :---------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------- |
| `Schema` _extends_ `object`                                                                     | -                                                                                      |
| `TQuery` _extends_ [`Query`](../../types-1/interfaces/interface.Query.md)\< `Schema`, `Item` \> | -                                                                                      |
| `Item` _extends_ `object`                                                                       | [`DirectusField`](../../schema/type-aliases/type-alias.DirectusField.md)\< `Schema` \> |

## Source

[rest/commands/create/fields.ts:5](https://github.com/directus/directus/blob/7789a6c53/sdk/src/rest/commands/create/fields.ts#L5)