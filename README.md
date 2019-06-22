# PHP WebRequest
A simple library for making web requests with PHP. It can handle one or multiple requests in parallel.

## Usage
Include the file __WebRequest.php__ in your php file:

    require_once 'WebRequest.php';

### GET Request

    $reqs = new WebRequest("https://example.com");

### POST Request

    $reqs[] = new WebRequest("https://example.com", "POST",[
        'name' => 'John',
        'last_name' => 'Doe',
    ]);


### POST Request (Multipart)

    $reqs[] = new WebRequest("https://example.com", "POST",[
        'name' => 'John',
        'last_name' => 'Doe',
    ]);
    $req->setDataType(WebRequest::DATA_MULTIPART);

### Sending JSON data
    $reqs[] = new WebRequest("https://example.com/api/users/1", "PUT",[
        'name' => 'John',
        'last_name' => 'Doe',
    ], [
        'Authorization: Bearer MzFhYTNjZmM0NmJhMmMyNWYwYzIxZWIyNTE4ZTU5ZjNkMTk5Yzk0O'
    ]);
    $req->setDataType(WebRequest::DATA_JSON);

### Running the Requests and getting the result
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
