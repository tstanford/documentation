# Mermaid Example

## Sequence Diagram

``` mermaid
    sequenceDiagram
    participant A as End User
    participant B as Web Page
    participant C as Application

    A ->>+ B : Click login button
    B ->>+ C : authenticate()
    C ->> C :  check credentials
    alt credentials are correct
    C ->> C : set result to true
    else credentials are wrong
    C ->> C : set result to false
    end
    C ->>- B : return result
    B ->>- A : redirect browser


```
