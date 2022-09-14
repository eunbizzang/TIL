```

let header = document.querySelector('meta[name="_csrf_header"]').content;
let token = document.querySelector('meta[name="_csrf"]').content;


headers: {
    'header': header,
    'X-Requested-With': 'XMLHttpRequest',
    "Content-Type": "application/json",
    'X-CSRF-Token': token
}
```

https://velog.io/@ybj1227/fetch-api
