# RISM Online API

The RISM Online API can be used to retrieve machine-readable representations of all available resources
in the RISM data. Every URL has both human-readable and a machine-readable representation, and these
may be changed by adjusting the `Accept` HTTP request header; a technique known as "Content Negotiation".

By default, the RISM Online service will deliver HTML-based representations of the content, suitable for the
majority of our users to browse and use the website. Under the hood, your browser is sending an `Accept` header
of `text/html`, which signals to our server that it should respond with the HTML version of a particular URL.

If we change the value of the `Accept` header to ask for a JSON representation using `application/ld+json`, 
the server will respond with a more machine-friendly representation of the same data in JSON-LD format.

Any standard HTTP client will have the facilities to do this. If you have the `curl` command available through the
command-line terminal in your local machine, you can experiment with this very easily.

    $ curl -H "Accept: application/ld+json" https://rism.online/sources/1001145660

This will return a response containing JSON-LD. If you vary this with:

    $ curl -H "Accept: text/html" https://rism.online/sources/1001145660

You will get an HTML response.

> Note: The HTML response you receive will not be suitable for "scraping"
> the page for information. When the HTML page loads it runs our 
> User Interface web application, which in turn performs a JSON request to
> retrieve the data from the API and update the page dynamically. If you load the page
> in your browser, this process is transparent to the user, but if you load the HTML page from the API
> you will only retrieve an unfilled template response.
> 
> Since all the data you would retrieve from scraping the HTML is available in the
> JSON-LD response, it is highly recommended that you use the API. If there is something
> that you are not finding in the API, [please let us know](https://github.com/rism-digital/rism-online-issues/issues/).

## Search and Resource APIs

There are two sections of the RISM Online API. The [Search API](search-api.md) provides a method of interacting with the RISM 
Online search system. With this API users can apply queries and filters to retrieve lists of results for all records 
accessible in RISM Online. Results in the Search API are returned in JSON-LD, so they may be parsed and manipulated 
as needed.

The second section, the [Resource API](resource-api.md) provides users with the ability to retrieve JSON-LD representations of 
records in RISM Online. With these representations users may extract any and all data from RISM records that they may 
be interested in.

It may be useful to note that the [RISM Online web interface](https://rism.online) uses the same public APIs described 
here. Any data you see in the web interface can be found using the public APIs. Almost all URLs in the public interface
also have a machine-readable counterpart, allowing users to experiment with their searches in the user interface, and 
then move their experiments into code later on. Notably, this includes the incipit search. 

## Multi-Lingual Support

To help ensure a consistent set of terminology across all languages for RISM resources, the API delivers all content
with JSON-LD Language Maps. This provides API users with a mechanism for showing human-readable labels for RISM data 
in their own systems, using terminology consistent with RISM itself. This is covered in the 
[languages documentation](languages.md).