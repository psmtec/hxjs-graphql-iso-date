# hxjs-graphql-iso-date

Haxe externs for https://github.com/excitement-engineer/graphql-iso-date


## usage

Add the 3 provided scalars to your schema.

```haxe
var schema = '
  scalar Date
  scalar Time
  scalar DateTime
  
  ...
  
  type Thing {
    name: String!
    createdAt: DateTime!
  }
  
  type Query {
    allTheThings: [Thing!]!
  }
  
  schema {
    query: Query
  }
';
```

Add the externs to your root resolver and just supply it some dates.

```haxe
...
var root = {
  Date: GraphQLDate,
  Time: GraphQLTime,
  DateTime: GraphQLDateTime,

  Query: {
    allTheThings: function( obj, args, context, info )
      return new js.Promise(function( resolve, reject ) {
        resolve([
          { name: 'Foo', createdAt: Date.now() },
          { name: 'Bar', createdAt: Date.now() },
        ]);
      });
  }
...
```
