https://stackoverflow.com/questions/44564905/what-is-over-fetching-or-under-fetching

Over-fetching is fetching too much data, meaning there is data in the response you don't use.

Under-fetching is not having enough data with a call to an endpoint, forcing you to call a second endpoint.

-> In both cases, they are performance issues: you either use more bandwidth than ideal, or you are making more HTTP requests than ideal