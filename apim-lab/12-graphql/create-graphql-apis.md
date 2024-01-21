---
title: Create GraphQL APIs
parent: Adding APIs
has_children: false
nav_order: 1
---


## Adding a Synthetic GraphQL API

For this lab you will use the existing [*Star Wars* API](https://swapi.dev) as the HTTP backend for your GraphQL APIs. 

Copy the following contents to a new file (People.gql) on any folder on your machine. 
```
type Person {
    name:       String!
    mass:       Int
    height:     Int
    hair_color: String
    skin_color: String 
    eye_color:  String 
    birth_year: String 
    gender:     String
    homeworld:  String
    url:        String 
}

type AllPeople {
    count:      Int!
    next:       String
    previous:   String
    results:    [Person]
}

type Query {
    getAllPeople: AllPeople
    getPerson(id: String): Person
}
```


- On the left menu, open the *APIs* blade. You will see all APIs, In the "Add API" screen select "GraphQL".

  ![APIM APIs](../../assets/images/add_graphql_api.png)

### Add GraphQL API

1) Click on **Add API**.  
2) Enter **Display name** `People`, **Name** `people`.  
3) For the GraphQL type, select **Synthetic GraphQL**.  
4) For the schema file, browse and upload the GraphQL schema (People.gql).  
5) Set the **API URL suffix** to `swgql`. This allows us to compartmentalize the Azure API Management URLs for distinct APIs.  
6) Press **Create**.

  ![APIM APIs](../../assets/images/create_graphql_from_schema.png)
