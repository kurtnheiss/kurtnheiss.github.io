```
openapi: 3.0.0
info:
  title: Dad Jokes API search endpoint
  description: |-
    The Dad Jokes API search endpoint searches for a dad joke using a term or word that may be present in the joke.
  termsOfService: https://www.icanhazdadjoke.com
  version: 1.0.0
servers:
  - url: https://www.icanhazdadjoke.com
externalDocs:
  description: Dad Jokes API Tutorial
  url: https://kurtnheiss.github.io/dad_jokes_files/dad_jokes.html#search-for-dad-jokes
paths:
  /search:
    get:
      summary: Searches the Dad Jokes API endpoint for dad jokes containing a specific term or word
      description: Retrieves dad jokes based on the specified search term or word.
      parameters:
        - name: term
          in: query
          required: true
          description: The search term to filter dad jokes.
          schema:
            type: string
      responses:
        '200':
          description: Dad jokes based on the search term are returned.
          content:
            application/json:
              schema:
                type: object
                properties:
                  current_page:
                    type: integer
                    description: The current page of the search results.
                  limit:
                    type: integer
                    description: The maximum number of jokes returned per page.
                  next_page:
                    type: integer
                    description: The next page number if available.
                  previous_page:
                    type: integer
                    description: The previous page number if available.
                  results:
                    type: array
                    items:
                      type: object
                      properties:
                        id:
                          type: string
                          description: The unique ID of the joke.
                        joke:
                          type: string
                          description: The text of the dad joke.
                  search_term:
                    type: string
                    description: The search term used to filter jokes.
                  status:
                    type: integer
                    description: The status code of the response.
                  total_jokes:
                    type: integer
                    description: The total number of jokes matching the search term.
                  total_pages:
                    type: integer
                    description: The total number of pages of search results.
        '502': 
          description: (3) URL rejected Malformed input to a URL function'
```
      

