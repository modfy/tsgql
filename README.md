# tsgql
Making Typescript and GraphQL a pleasant experience.

## What is this?
tsgql is a GraphQL code generator that takes a different approach, instead of generating types from your GraphQL schema, you define your Typescript types first and use that to generate the schema.

This allows you to use the flexibility and expressiveness of Typescript's type system to create GraphQL schemas, unlike alternatives such as [type-graphql](https://github.com/MichalLytek/type-graphql), which force you to use clunky and cumbersome classes/decorators.

It allows you to do things like this:
```typescript
export type User = {
  id: string;
  name: string;
  age: number;
};

export type Mutation = {
	updateUser: (args: { id: User['id'], fields: Partial<Omit<User, 'id'>> }) => Promise<User>
}
```
Which generates the following GraphQL schema:
```graphql
type User {
  id: String!
  name: String!
  age: Int!
}

input UpdateUserInputFields {
  name: String
  age: Int
}

type Mutation {
  updateUser(id: String!, fields: UpdateUserInputFields!): User!
}

```