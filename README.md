# ts-sync-request
## TypeScript strongly-typed wrapper for sync-request library

## Make synchronous http calls in TypeScript

The package exports **SyncRequestClient** and **SyncRequestService** classes which have methods to make synchronous Http GET, POST calls from TypeScript.

[**sync-request library on npm**](https://www.npmjs.com/package/sync-request)

[**ts-sync-request library on npm**](https://www.npmjs.com/package/ts-sync-request)

## Sample usage

**TypeScript classes**

```typescript
class Request
{
    Email: string;
}

class Response
{
    isValid: boolean;
}
```

**Usage**

### Fluent API

You can use the fluent API by using the **SyncRequestClient** class as shown below.

```typescript
import { SyncRequestClient } from 'ts-sync-request/dist'
```

**GET**:

```typescript
    let email = "jdoe@xyz.com";
    let url = "http://localhost:59039/api/Movies/validateEmail/" + email;

    let response = new SyncRequestClient()
                                .addHeader("Authorization", "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1NDc2OTg1MzgsIm5iZiI6MTU0NzY5NDIxOCwiaHR0cDovL3NjaGVtYXMueG1sc29hcC5vcmcvd3MvMjAwNS8wNS9pZGVudGl0eS9jbGFpbXMvbmFtZSI6InN0cmluZyIsImh0dHA6Ly9zY2hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6InN0cmluZyIsIkRPQiI6IjEvMTcvMjAxOSIsImlzcyI6InlvdXIgYXBwIiwiYXVkIjoidGhlIGNsaWVudCBvZiB5b3VyIGFwcCJ9.qxFdcdAVKG2Idcsk_tftnkkyB2vsaQx5py1KSMy3fT4")
                            .get<Response>(url);
```

**POST**:

```typescript
    let url = "http://localhost:59039/api/Movies/validateEmailPost";
    let request = new Request();
    request.Email = "jdoe@xyz.com";

    let response = new SyncRequestClient()
                                .addHeader("Authorization", "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1NDc2OTg1MzgsIm5iZiI6MTU0NzY5NDIxOCwiaHR0cDovL3NjaGVtYXMueG1sc29hcC5vcmcvd3MvMjAwNS8wNS9pZGVudGl0eS9jbGFpbXMvbmFtZSI6InN0cmluZyIsImh0dHA6Ly9zY2hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6InN0cmluZyIsIkRPQiI6IjEvMTcvMjAxOSIsImlzcyI6InlvdXIgYXBwIiwiYXVkIjoidGhlIGNsaWVudCBvZiB5b3VyIGFwcCJ9.qxFdcdAVKG2Idcsk_tftnkkyB2vsaQx5py1KSMy3fT4")
                            .post<Request, Response>(url, request);
```

The **addHeader** API is optional. You can call **addHeader** multiple times to add multiple headers.

### Traditional API

You can use the traditional API by using the **SyncRequestService** class as shown below.

```typescript
import { SyncRequestService, SyncRequestHeader } from 'ts-sync-request/dist';
```

**GET**:

```typescript
    let email = "jdoe@xyz.com";
    let url = "http://localhost:59039/api/Movies/validateEmail/" + email;

    // Add headers
    let header = new SyncRequestHeader("Authorization", "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1NDc2OTg1MzgsIm5iZiI6MTU0NzY5NDIxOCwiaHR0cDovL3NjaGVtYXMueG1sc29hcC5vcmcvd3MvMjAwNS8wNS9pZGVudGl0eS9jbGFpbXMvbmFtZSI6InN0cmluZyIsImh0dHA6Ly9zY2hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6InN0cmluZyIsIkRPQiI6IjEvMTcvMjAxOSIsImlzcyI6InlvdXIgYXBwIiwiYXVkIjoidGhlIGNsaWVudCBvZiB5b3VyIGFwcCJ9.qxFdcdAVKG2Idcsk_tftnkkyB2vsaQx5py1KSMy3fT4");
     
    let headers: SyncRequestHeader[] = new Array<SyncRequestHeader>();
    headers.push(header);     

    let response = new SyncRequestService().get<Response>(url, headers);
```

**POST**:

```typescript
    let url = "http://localhost:59039/api/Movies/validateEmailPost";
    let request = new Request();
    request.Email = "jdoe@xyz.com";

    // Add headers
    let header = new SyncRequestHeader("Authorization", "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1NDc2OTg1MzgsIm5iZiI6MTU0NzY5NDIxOCwiaHR0cDovL3NjaGVtYXMueG1sc29hcC5vcmcvd3MvMjAwNS8wNS9pZGVudGl0eS9jbGFpbXMvbmFtZSI6InN0cmluZyIsImh0dHA6Ly9zY2hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6InN0cmluZyIsIkRPQiI6IjEvMTcvMjAxOSIsImlzcyI6InlvdXIgYXBwIiwiYXVkIjoidGhlIGNsaWVudCBvZiB5b3VyIGFwcCJ9.qxFdcdAVKG2Idcsk_tftnkkyB2vsaQx5py1KSMy3fT4");
     
    let headers: SyncRequestHeader[] = new Array<SyncRequestHeader>();
    headers.push(header);     

    let response = new SyncRequestService().post<Request, Response>(url, request, headers);
```
 
The **headers** parameter is optional.

## Options

Below options are supported.

| Option | Default | Description |
| ---- | ---- | ---- |
| followRedirects | true | can be explicitly set to false to prevent following redirects automatically. |
| maxRedirects | Infinity | sets the maximum number of redirects. |
| timeout | false | times out if no response is returned within the given number of milliseconds. |
| retry | false | retry GET requests. Set this to true to retry when the request errors or returns a status code greater than or equal to 400 |
| retryDelay | 200 | the delay between retries in milliseconds. |
| maxRetries | 5 | the number of times to retry before giving up. |

These options are available via the **SyncRequestOptions** class. You can set them as you want.

```typescript
import { SyncRequestClient, SyncRequestOptions } from 'ts-sync-request/dist'
```

```typescript
    let email = "jdoe@xyz.com";
    let url = "http://localhost:59039/api/Movies/validateEmail/" + email;

    let options = <SyncRequestOptions> { 
        timeout: true
    };

    let response = new SyncRequestClient(options)
                                .addHeader("Authorization", "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1NDc2OTg1MzgsIm5iZiI6MTU0NzY5NDIxOCwiaHR0cDovL3NjaGVtYXMueG1sc29hcC5vcmcvd3MvMjAwNS8wNS9pZGVudGl0eS9jbGFpbXMvbmFtZSI6InN0cmluZyIsImh0dHA6Ly9zY2hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6InN0cmluZyIsIkRPQiI6IjEvMTcvMjAxOSIsImlzcyI6InlvdXIgYXBwIiwiYXVkIjoidGhlIGNsaWVudCBvZiB5b3VyIGFwcCJ9.qxFdcdAVKG2Idcsk_tftnkkyB2vsaQx5py1KSMy3fT4")
                            .get<Response>(url);
```