https://stackoverflow.com/questions/8648892/how-to-convert-url-parameters-to-a-javascript-object


```
var search = location.search.substring(1);
JSON.parse('{"' + decodeURI(search).replace(/"/g, '\\"').replace(/&/g, '","').replace(/=/g,'":"') + '"}')

```