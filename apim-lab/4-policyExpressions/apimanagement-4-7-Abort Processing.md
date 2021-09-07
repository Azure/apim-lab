---
title: Abort processing policy
parent: Policy Expressions
has_children: false
nav_order: 7
---



## Calculator API

### Aborting the processing

- Open the Calculator API 'Code View'
- Add the inbound policy to test for a condition and return an error
- Invoke the API - with Authorization header as above ... should get a 599 error
- Replace the condition with some more meaningful code

```xml
<!-- Inbound -->
<choose>
    <when condition="@(true)">
        <return-response response-variable-name="existing response variable">
            <set-status code="599" reason="failure" />
            <set-header name="failure" exists-action="override">
                <value>failure</value>
            </set-header>
            <set-body>blah</set-body>
        </return-response>
    </when>
</choose>
```

![](../../assets/images/APIMResponseAbort.png)