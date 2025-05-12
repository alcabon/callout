# callout

```mermaid
sequenceDiagram
    participant User
    participant LWC as LWC Component
    participant Apex as ContinuationCalloutController
    participant External as External Service

    User->>LWC: Click “Call API” button
    LWC->>LWC: showSpinner = true
    LWC->>Apex: startLongRunningRequest()
    Apex->>Apex: new Continuation(timeout, callback) [2]
    Apex->>External: HttpRequest added to Continuation [2]
    Note right of Apex: Original Apex transaction ends
    External-->>Apex: HTTP response arrives later
    Apex->>Apex: handleResponse(labels, state) retrieves HttpResponse [2]
    Apex-->>LWC: return response body
    LWC->>LWC: showSpinner = false; display result
```
