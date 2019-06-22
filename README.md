# PHP WebRequest
A simple library for making web requests with PHP. It can handle one or multiple requests in parallel.
This library is a work in progress.

## Usage
Include the file __WebRequest.php__ in your php file:

```php
require_once 'WebRequest.php';
```

### GET Request

```php
$reqs = new WebRequest("https://example.com");
```

### POST Request

```php
$reqs[] = new WebRequest("https://example.com", "POST",[
    'name' => 'John',
    'last_name' => 'Doe',
]);
```

### POST Request (Multipart)

```php
$reqs[] = new WebRequest("https://example.com", "POST",[
    'name' => 'John',
    'last_name' => 'Doe',
]);
$req->setDataType(WebRequest::DATA_MULTIPART);
```

### Sending JSON data
    
```php
$reqs[] = new WebRequest("https://example.com/api/users/1", "PUT",[
    'name' => 'John',
    'last_name' => 'Doe',
], [
    'Authorization: Bearer MzFhYTNjZmM0NmJhMmMyNWYwYzIxZWIyNTE4ZTU5ZjNkMTk5Yzk0O'
]);
$req->setDataType(WebRequest::DATA_JSON);
```

### Running the Requests and getting the result

```php
// Single request
$req->request();
// Do something with $req->getResponse()

// Multiple requests.
WebRequests::requestAll($reqs);
// At this point every request has completed.
// Do something with the responses
foreach ($reqs as $req){
    // Do something with $req->getResponse()
}
```