# ServiceNow Filters

## Filter Searches

|Condition to search - Description  | Search Parameters - Wildcard |
|---|---|
|Search for values that contain search-term. |<li>*search-term</li><li>%searchterm%</li>|
|Search for values that end with search-term.|<li>%search-term</li> |
|Search for values that start with search-term.|<li>search-term%</li> |
|<b>Search for values than don't start with search-term.</b>|<li>!=STARTSWITHsearch-term</li> |
|Search for values that equal search-term.|<li>=search-term</li> |
|Search for values that do not contain search-term.|<li>!*searchterm</li> |
|Search for values that do not end with search-term.|<li>!%searchterm</li> |
|Search for values that do not equal searchterm.|<li>!=searchterm</li> |


This search supports queries that include AND, but does not support OR. You cannot search in a column that uses the List field type, for example, watch lists.

- Procedure
 1. Click the search icon Search icon to expand the column headers and add a search field to each column.
 2. To search a single column, enter the search text in the desired column search field and press the Enter key. Use wildcards to further refine column searches. For example, use the * to define a contains search.
 3. To search multiple columns, perform one of the following actions.
    1. Enter the search text in each of the desired column search fields and press the Enter key.
    2. Search an individual column and then search additional columns based on the results of the first search.
- Result : The search returns records that match the search term. What to do next
    To clear a column search, complete one of the following actions.
  - Delete the text in the search field for the desired column and press the Enter key. This returns results for any remaining column search criteria.
  - Delete the text in all of the column search fields to return all records in the list.




