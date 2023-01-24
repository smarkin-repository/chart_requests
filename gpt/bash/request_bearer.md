
Could you prepare simple example  request with bearer token  on python. I think the example includes two function, one for getting bearer token, second for request with bearer token. You can use some gateway server with random name.

```
#!/bin/bash

check_jq(){
    # check if jq is installed
    if ! [ -x "$(command -v jq)" ]; then
        echo "Error: jq is not installed. Please install it before running this script."
        exit 1
    fi
}

# Function for retrieving a bearer token
get_bearer_token() {
    local endpoint=$1
    local client_id=$2
    local client_secret=$3

    # Retrieve a bearer token
    local response=$(curl -s -X POST -H "Content-Type: application/json" -d "{\"client_id\":\"$client_id\",\"client_secret\":\"$client_secret\"}" $endpoint)
    local bearer_token=$(echo $response | jq -r .access_token)
    echo $bearer_token
}

# Function for making a request with a bearer token
make_request() {
    local endpoint=$1
    local bearer_token=$2

    # Make a request with a bearer token
    local response=$(curl -s -H "Authorization: Bearer $bearer_token" $endpoint)
    echo $response
}

# check if jq is installed
check_jq

# Example endpoint for retrieving a bearer token
token_endpoint="https://example-gateway-server.com/token"

# Get the bearer token
bearer_token=$(get_bearer_token $token_endpoint "example_client_id" "example_client_secret")

# Example endpoint for making a request
data_endpoint="https://example-gateway-server.com/data"

# Make a request with the bearer token
data=$(make_request $data_endpoint $bearer_token)

# Print the data
echo $data
```