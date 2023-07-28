---
editLink: false
---

# Type alias: CreateFileOutput`<Schema, TQuery, Item>`

> **CreateFileOutput**: \<`Schema`, `TQuery`, `Item`\>
> [`ApplyQueryFields`](../../types-1/type-aliases/type-alias.ApplyQueryFields.md)\< `Schema`, `Item`,
> `TQuery`[`"fields"`] \>

## Type parameters

| Parameter                                                                                       | Default                                                                              |
| :---------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------- |
| `Schema` _extends_ `object`                                                                     | -                                                                                    |
| `TQuery` _extends_ [`Query`](../../types-1/interfaces/interface.Query.md)\< `Schema`, `Item` \> | -                                                                                    |
| `Item` _extends_ `object`                                                                       | [`DirectusFile`](../../schema/type-aliases/type-alias.DirectusFile.md)\< `Schema` \> |

## Source

[rest/commands/create/files.ts:5](https://github.com/directus/directus/blob/7789a6c53/sdk/src/rest/commands/create/files.ts#L5)