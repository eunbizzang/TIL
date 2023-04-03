https://momentjs.com/


Format Dates
```
moment().format('MMMM Do YYYY, h:mm:ss a'); // April 3rd 2023, 10:54:19 am
moment().format('dddd');                    // Monday
moment().format("MMM Do YY");               // Apr 3rd 23
moment().format('YYYY [escaped] YYYY');     // 2023 escaped 2023
moment().format();                          // 2023-04-03T10:54:19+09:00
```


Relative Time
```
moment("20111031", "YYYYMMDD").fromNow(); // 11 years ago
moment("20120620", "YYYYMMDD").fromNow(); // 11 years ago
moment().startOf('day').fromNow();        // 11 hours ago
moment().endOf('day').fromNow();          // in 13 hours
moment().startOf('hour').fromNow();       // an hour ago
```


Calendar Time
```
moment().subtract(10, 'days').calendar(); // 03/24/2023
moment().subtract(6, 'days').calendar();  // Last Tuesday at 10:54 AM
moment().subtract(3, 'days').calendar();  // Last Friday at 10:54 AM
moment().subtract(1, 'days').calendar();  // Yesterday at 10:54 AM
moment().calendar();                      // Today at 10:54 AM
moment().add(1, 'days').calendar();       // Tomorrow at 10:54 AM
moment().add(3, 'days').calendar();       // Thursday at 10:54 AM
moment().add(10, 'days').calendar();     
```