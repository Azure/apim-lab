---
title: Mock policy
parent: Policy Expressions
has_children: false
nav_order: 5
---



## Star Wars API

### Mock responses

Mocking provides a way to return sample responses even when the backend is not available. This enables app developers to not be help up if the backend is under development.

- Open the Star Wars API and select [Add Operation]
- Create a new operation called GetFilm
- In the Response configuration tab, set Sample data as below

![](../../assets/images/APIMMockingFrontend.png)

![](../../assets/images/APIMMockingFrontend2.png)

![](../../assets/images/APIMMockingFrontend3.png)

```json
{
  "count": 1,
  "films": [   { "title": "A New Hope",  "blah": "xxx"    }   ]
}
```

- Open the Inbound processing 'Code View'
- Enable mocking and specify a 200 OK response status code

![](../../assets/images/APIMMockingInbound.png)

- Select the 200 OK response ... Save

![](../../assets/images/APIMMockingInbound2.png)

- Mocking is now enabled

![](../../assets/images/APIMMockingInbound3.png)

- Invoke the API ... should get a 200 success with the mocked data

![](../../assets/images/APIMMockingResponse.png)
