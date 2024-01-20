---
title: Create GraphQL APIs
parent: Adding APIs
has_children: false
nav_order: 1
---


## Adding a Synthetic GraphQL API

For this lab you willuse the existing [*Star Wars* API](https://swapi.dev) as the HTTP backend for your GraphQL APIs. 

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
    gender:		String
    homeworld:	String
    url:		String 
}

type AllPeople {
    count:      Int!
    next:       String
    previous:   String
    results: [Person]
}

type Query {
    getAllPeople: AllPeople
    getPerson(id: String): Person
}
```


- On the left menu, open the *APIs* blade. You will see all APIs, the possibility to add new ones, but also to customize existing ones.

  ![APIM APIs](../../assets/images/apim-apis.png)

### Add API from Scratch

Instead of developing an API, for this lab you will use the existing [*Star Wars* API](https://swapi.dev):

1) Click on **Add API**.  
2) Click on **HTTP - Manually define an HTTP API**.  
3) Select the **Full** option in the **Create an HTTP API** dialog.  
4) Enter **Display name** `Star Wars`, **Name** `star-wars`, and, optionally, **Description**.  
5) Assign `https://swapi.dev/api` to the **Web service URL**.  
6) Keep the **URL scheme** at `HTTPS` as we strive to enforce HTTPS only.  
7) Set the **API URL suffix** to `sw`. This allows us to compartmentalize the Azure API Management URLs for distinct APIs.  
8) Assign **Starter** and **Unlimited** products.  
9) Press **Create**.  
