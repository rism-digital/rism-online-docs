The Sigla API is a small convenience API that can help RISM users resolve the [RISM sigla](https://rism.info/community/sigla/about.html) to an institution record. 

There are two components: A **sigla resolver** and a **sigla query API**. The sigla resolver will redirect a URL with the
RISM siglum of an institution to the RISM Online record for that institution.

For example, `https://rism.online/sigla/GB-Lbl` will redirect the user to `https://rism.online/institutions/30001581`, the authority record for the British Library. All RISM sigla will have an authority record. If a siglum is entered that does not exist, a `404 Not Found` response is returned. 

For the query API, this is similar to the full search API but with a restricted set of query parameters. The query parameter, `q`, takes the search term. An optional query type parameter, `qt`, changes the fields that are searched. The available query types are: `all`, `siglum`, `name`, `city`, and `country`. If the `qt` parameter is not supplied, the `all` value is assumed. Finally, the `page` query parameter lets the user page through the results, twenty results at a time. 

The `siglum` query type will match queried sigla, but attempt to match it from the left. Partial sigla are therefore matched.

No sorting of results is available. The default sorting is by relevance, with a slight boost for institutions that have larger holdings.

The results are returned in the same JSON-LD format as the Search API. See the section in the [Search API](search-api.md) documentation on Parsing Search API Responses.

Here are some examples of search queries.

`https://rism.online/sigla/?q=kloster`: Search all institution records for the word "kloster" anywhere in the record.

`https://rism.online/sigla/?q=GB-O&qt=siglum`: Search all institutions that start with "GB-O" (i.e., all institutions in Oxford, UK).

`https://rism.online/sigla/?q=archives&qt=name`: Search all institutions with "archives" in the name.