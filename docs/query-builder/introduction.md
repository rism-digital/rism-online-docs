# The Query Builder

The Keyword Query field will search a broad combination of fields that have been specifically selected to meet the needs of most users. However, for users with specific search needs, the Keyword Query field can also be used to build more expressive queries. 

The Query Builder tool helps guide users in creating expressive queries for searching the RISM data. Once familiar with the syntax, users may simply input these queries into the Keyword Query field directly, without needing to use the Query Builder.

## Term and Phrase queries

There are two broad types of query: A **term** query, and a **phrase** query. A term query is one or more words in the Keyword Query field. This will be interpreted with an implicit "AND" between each term. An example might be: `beethoven opera fidelio`. When the search system interprets this query, it will look for records that contain the words `beethoven` AND `opera` AND `fidelio` anywhere in the record. At the time of writing, this search returns around 200 results.

By contrast, a phrase query is enclosed in quotation marks and looks for a specific sequence of words together. (They must be the double quotation marks -- single marks are not supported.) The same query as above, entered as a phrase query, returns no results. However, if we take the phrase `"Erste Bearbeitung, mit Korrekturen von der Hand"`, this will return the record(s) that contain this exact phrase. 

## Searching specific fields

Each record type (Sources, People, Institutions, and Incipits) has a number of fields available for specific queries; for example, a publisher number or a watermark description on a source. The Query Builder shows a list of the fields available. Clicking on a field will insert the field name into the query box. Users can then supply the specific query they want for this field. The field and the query are separated by a colon, `:`. 

Field queries support both term and phrase queries, with one notable caveat: For multiple terms in a field search, the field must be specified for each term. For example, if you wish to search the "Watermark" field for several terms, the term query: `watermark:anchor key` will be interpreted as `watermark:anchor` and `any field: key`. If you wish to search for both of these terms in the watermark field, it must be `watermark:anchor watermark:key`. (An implicit AND is inserted between the two statements). Fielded phrase queries do not need this, so the query `watermark:"Anchor in circle"` will find this specific phrase in the watermark field.

## Basic operators

We have already seen that an implicit `AND` operator is inserted between terms. The `AND` operator requires that both terms are present in a record for it to match. The `OR` operator only requires that one or the other term match. So a search for `mozart AND symphony` will return records that contain both of these terms, while a search for `mozart OR symphony` will return results where the record has either of those terms.

The `NOT` operator negates the term, specifying that it must not be present. `mozart NOT symphony` will only return records that have the term `mozart` but not the term `symphony`.

For `AND`, `OR`, and `NOT` operators, they must be specified in upper-case (majuscule) letters. They will be interpreted as a term in the search if they are given in lower-case (miniscule).

Also available are the `+` and `-` operators. These place a requirement that a term must, or must not, be in a record. So a search for `mozart AND symphony +jupiter` will return records that have both `mozart` and `symphony`, with the additional requirement that these records must contain the word `jupiter`. Likewise, `mozart AND symphony -jupiter` will return records that match the first part, but do not contain the word `jupiter`. 

The `+` operator is similar to the `AND` operator, but with no expectation that the terms must balance -- `+jupiter` is a valid query, whereas `AND jupiter` is not. The `-` operator is, likewise, functionally similar to the `NOT` operator. 

## Wildcards

The wildcard operator provides a way of matching inexact queries where variations in spelling may otherwise not return a match. There are two wildcard operators: `?` will match a single character, while `*` will match one or more characters. For example, `V?ndome` will match both "Vendome" and "Vandome", while `Symphon*` will match "Symphonies" and "Symphony".

A special type of wildcard is also available, `fieldname:[* TO *]`. This provides a way of querying for any record that contains a value in a specific field. So `series:[* TO *]` will return all records that have any value in the RISM Series Statement field.

## Boosting and Proximity operators

The "Boost" operator, `^`, provides a way for a user to weight a given term or phrase using a numerical value, making them appear higher in the results. It does not change the number of results, it changes the order in which those results are presented. An example might be a query `"Six Quatuors" Violon^20`. This will look for the phrase `"Six Quartors"` and the term `Violon` anywhere in the record, but will bring records that mention the term `Violon` to the top of the results. Any postitive decimal number is a valid boost value.

Without a specific value, the boost value is interpreted as `1.0` ("no boost"). A boost value smaller than 1 will provide a negative boost, weighting these terms lower in the list, e.g., `"Six Quatuors" Violon^0.1` will push the records that mention `Violon` towards the end of the results lis

The "Proximity" operator, `~`, also takes a numerical value and has two functions. For term queries, this provides a way of specifying an "edit distance" for that term; that is, an upper limit on the number of transformations that can be considered a match. For example, `haydn~3` would match `haidn, hayden, heyden, maydn, haydin`, etc, since all of these terms contain less than three changes to transform them from the original query; that is `haydn -> haidn` is one operation, the `y` changed to an `i`.

For phrase queries, the proximity operator provides a certain amount of "slop" in the phrase, which is the distance from one word to another within the phrase. `"symphony C minor"~5` would match a record where any of those terms occur within five words of each other.

## Grouping

Terms, phrases, and fields can be grouped together with parentheses to provide way of combining operators in increasingly specific ways. `Hensel AND (Marx OR Moscheles) NOT Felix` will find records that mention Hensel and Marx or Moscheles, but not Felix.

## Examples

- `series:2640 AND creator:Pleyel`: Search the RISM Series field for the RISM identifier '2640', where "Pleyel" is listed as the primary composer. 
- `watermark:anchor creator:Mozart -Breitkopf`: Retrieve sources with the term 'anchor' in the watermark field, where the creator has the term "Mozart", but the term "Breitkopf" is not in the record.
- `creator:Wein*`: Retrieve all records where the creator name matches "Wein..." with any ending.

