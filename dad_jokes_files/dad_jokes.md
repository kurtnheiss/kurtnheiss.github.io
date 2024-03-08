# Dad Jokes API Tutorial

* [Overview](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#overview)
  * [Resource details](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#resource-details)
  * [Header format](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#header-format)
  * [User agent](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#user-agent)
* [Dad joke requests](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#dad-joke-requests)
  * [Obtain a random dad joke](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#obtain-a-random-dad-joke)
  * [Obtain a specific dad joke](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#obtain-a-specific-dad-joke)
  * [Obtain a dad joke as an image](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#obtain-a-dad-joke-as-an-image)
  * [Search for dad jokes](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#search-for-dad-jokes)
      * [Pagination](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#pagination)
  * [Obtain a joke using GraphQL](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#obtain-a-joke-by-graphql-query)
* [Error handling](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#error-handling) 
 
## Overview
The Dad Joke REST API enables you to access a vast database of dad jokes to obtain:

* A random dad joke
* A random dad joke formatted for Slack
* A specific dad joke
* A dad joke as an image
* A list of dad jokes

### Resource details
The Dad Jokes API is located at [https://icanhazdadjoke.com](https://icanhazdadjoke.com).

No authentication is required to use the Dad Jokes API.

In this tutorial the `curl` command is used for Dad Jokes API requests and the JSON format for the response output.

> **NOTE:** Python, JavaScript, Java, Ruby, and other popular programming languages can be used to make HTTP requests to the Dad Joke API endpoints; however, these languages are out of the scope of and not included in this tutorial.

### Header format
Valid `Accept` headers include:
* `text/html` - HTML response (default response format)
* `application/json` - JSON response
* `text/plain` - Plain text response

> **IMPORTANT:** `curl` requests made without a valid `Accept` header receive a `text/plain` response.

### User agent
The Dad Joke API requires that you set a custom `User-Agent` header for all requests. By setting a custom `User-Agent` header for your code you facilitate usage monitoring and helps the server understand the capabilities and 
context of the client making the request.

Your user agent should include the name of the library or website that is accessing the API along with a contact URL or e-email.

Inclusion of the user agent in the API request has the following format:

```
$ curl -H "User-Agent: My Library (https://github.com/username/repo)" https://icanhazdadjoke.com/
```
For example:
```
url -H "User-Agent: MyCoolApp/1.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.182 Safari/537.36" https://icanhazdadjoke.com/
```
> **IMPORTANT:** The following requests with examples in this tutorial do not incorporate use the use of a `User-Agent` for the sake of brevity and clarity.**

## Dad Joke requests
The following sections describe some of the requests you can make to the Dad Joke endpoint:

* [Obtain a random dad joke](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#obtain-a-random-dad-joke)
* [Obtain a random dad joke as a Slack message](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#obtain-a-random-dad-joke-formatted-for-slack)
* [Obtain a specific dad joke](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#obtain-a-specific-dad-joke)
* [Obtain a dad joke as an image](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#obtain-a-dad-joke-as-an-image)
* [Search for dad jokes](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#search-for-dad-jokes)
  * [Pagination](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#pagination) 
* [Obtain a joke by GraphQL query](https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#obtain-a-joke-by-graphql-query)

### Obtain a random dad joke
To obtain a random dad joke, use the following command:
```
$ curl -H "Accept: application/json" https://icanhazdadjoke.com
```
Response:
```
{
  "id": "R7UfaahVfFd",
  "joke": "My dog used to chase people on a bike a lot. It got so bad I had to take his bike away.",
  "status": 200
}
```

### Obtain a random dad joke formatted for Slack
To obtain a random dad joke formatted for Slack, use the following command:
```
$ curl -H "Accept: application/json" https://icanhazdadjoke.com/slack.
```
Response:
```
{
  "attachments": [
    {
      "fallback": "What kind of magic do cows believe in? MOODOO.",
      "footer": " - ",
      "text": "What kind of magic do cows believe in? MOODOO."
    }
  ],
  "response_type": "in_channel",
  "username": "icanhazdadjoke"
}
```
### Obtain a specific dad joke
To obtain a specific Dad Joke you use the `<joke_id>` parameter in the following request format:

```
$ curl -H "Accept: application/json" https://icanhazdadjoke.com/j/<joke_id>
```
Using the `joke_id` value of `R7UfaahVfFd` shown in a previous example you make the following request:
```
$ curl -H "Accept: application/json" https://icanhazdadjoke.com/j/R7UfaahVfFd 
```
Response:
```
{
  "id": "R7UfaahVfFd",
  "joke": "My dog used to chase people on a bike a lot. It got so bad I had to take his bike away.",
  "status": 200
}
```
### Obtain a dad joke as an image
To obtain a dad joke as an image, append the `<joke_id>` parameter with `.png` and make the following request:
```
$ curl -H "Accept: application/json" https://icanhazdadjoke.com/j/<joke_id>.png
```
Using the `joke_id` value of `R7UfaahVfFd` shown in a previous example you make the following request:
```
$ curl -H "Accept: application/json" https://icanhazdadjoke.com/j/R7UfaahVfFd.png
```
Response:
```
<img src="https://icanhazdadjoke.com/j/R7UfaahVfFd.png" />
```
 
### Search for dad jokes
To search for a dad joke using a term or word that may be present in the joke, append the Dad Joke API request with `search` and `term` as shown:
```
$ curl -H "Accept: application/json" https://icanhazdadjoke.com/search?term=<your_term>”
```
For example appending the Dad Joke URL with `search` and the `term` parameter in the following:
```
$ curl -H "Accept: application/json" https://icanhazdadjoke.com/search?term=bike”
```
Provides the following JSON response output:
```
{
  "current_page": 1,
  "limit": 20,
  "next_page": 1,
  "previous_page": 1,
  "results": [
    {
      "id": "R7UfaahVfFd",
      "joke": "My dog used to chase people on a bike a lot. It got so bad I had to take his bike away."
    },
    {
      "id": "HtcNuHJBQCd",
      "joke": "How many kids with ADD does it take to change a lightbulb? Let's go ride bikes!"
    }
  ],
  "search_term": "bike",
  "status": 200,
  "total_jokes": 2,
  "total_pages": 1
}
```

#### Pagination

You can control the pagination of your dad joke search using the `page` and `limit` parameters: 

* `page`: The current page of results to obtain (the default value is page 1)
* `limit`: The number of results to return per page (the default number of results to return per page is 20 with a maximum of 30)

For example, to see a limit of 10 dad jokes on the 3rd page of results you use the following command:
```
$ curl -H "Accept: application/json" "https://icanhazdadjoke.com/?page=3&limit=10"
```
Which generates the the following response showing all of the dad jokes on the 3rd page of results:
```
{"id":"FdN7wcxAskb","joke":"They're making a movie about clocks. It's about time","status":200}
```
Combining the `page` and `limit` parameters with `search` and `term` enables you to refine the dad joke output you are seeking.

For example:
```
$ curl -H "Accept: application/json" "https://icanhazdadjoke.com/search?term=bike&page=1&limit=10"
```
The JSON output is:
```
{
  "current_page": 1,
  "limit": 10,
  "next_page": 1,
  "previous_page": 1,
  "results": [
    {
      "id": "R7UfaahVfFd",
      "joke": "My dog used to chase people on a bike a lot. It got so bad I had to take his bike away."
    },
    {
      "id": "HtcNuHJBQCd",
      "joke": "How many kids with ADD does it take to change a lightbulb? Let's go ride bikes!"
    }
  ],
  "search_term": "bike",
  "status": 200,
  "total_jokes": 2,
  "total_pages": 1
}

```

### Obtain a joke by GraphQL query
You can obtain a specific joke and its text using a POST request sent to the Dad Joke API GraphQL endpoint. 
Using GraphQL for dad joke searches can lead to more efficient, flexible, and maintainable code compared to traditional RESTful approaches.

An example of the full curl command is as follows:
```
$ curl -X POST \ -H "Content-Type: application/json" \ --data '{"query": "{ joke { id, joke } }"}' \ https://icanhazdadjoke.com/graphql
```
The elements of note in this request are:

* `-H "Content-Type: application/json"`: This option sets the content type of the request header to JSON. It tells the server that the data being sent in the body is JSON formatted.
* `--data '{"query": "{ joke { id, joke } }"}'`: This option specifies the data payload of the POST request.
* `https://icanhazdadjoke.com/graphql`: This is the URL to which the `POST` request is being sent. It's a GraphQL endpoint hosted at `https://icanhazdadjoke.com`.

Using the previous example of `R7UfaahVfFd` the format of your GraphQL request is:
```
$ curl -X POST \ -H "Content-Type: application/json" \  --data '{"query": "{ joke(id: \"R7UfaahVfFd\") { id, joke } }"}' \ https://icanhazdadjoke.com/graphql
```
The following is a JSON output example for this type of request:
```
{"data":{"joke":{"id":"R7UfaahVfFd","joke":"My dog used to chase people on a bike a lot. It got so bad I had to take his bike away."}}}% 
```
## Error Handling
Successful requests to the Dad Jokes API provide the requested dad joke and associated details along with a `“status”: 200` message.

Malformed or incomplete requests receive an error message specifying the issue or problem with the request.

For example:
```
curl: (3) URL rejected: Malformed input to a URL function
```

