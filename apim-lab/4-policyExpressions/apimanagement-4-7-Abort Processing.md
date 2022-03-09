---
title: Abort processing policy
parent: Policy Expressions
has_children: false
nav_order: 7
---


## Calculator API

### Aborting the processing

The ability to terminate a response gracefully is of importance in a number of cases such as error handling or business logic. Using the `return-response` policies short-circuits the request and yields a response that often does not originate from the backend. Consider what general situations may make sense without shifting too much business logic into APIM.

- Open the Calculator API 'Code View'.
- Add the inbound policy to test for a condition and return an error.
- Invoke the API with the Authorization header as before. 
- Observe the 500 error.
- Replace the condition with more meaningful code.

  ```xml
  <inbound>
      <base />
      <choose>
          <when condition="@(true)">
              <return-response response-variable-name="existing response variable">
                  <set-status code="500" reason="Internal Server Error" />
                  <set-header name="failure" exists-action="override">
                      <value>failure</value>
                  </set-header>
                  <set-body>Internal Server Error</set-body>
              </return-response>
          </when>
      </choose>
  </inbound>
  ```

  ![APIM Policy Abort Response](../../assets/images/apim-policy-abort-response.png)