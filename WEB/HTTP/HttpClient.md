https://www.baeldung.com/apache-httpclient-vs-closeablehttpclient


HttpClient is a high-level interface that represents the basic contract for HTTP request execution. 


CloseableHttpClient is an abstract class that represents a base implementation of the HttpClient interface. 
However, it also implements the Closeable interface. 
Thus, we should close all its instances after use. 
We can close them by using either try-with-resources or by calling the close method in a finally clause:


```
try (CloseableHttpClient httpClient = HttpClients.createDefault()) {
     HttpGet httpGet = new HttpGet(serviceOneUrl);
     httpClient.execute(httpGet, response -> {
       assertThat(response.getCode()).isEqualTo(HttpStatus.SC_OK);
       return response;
     });
}
```
Therefore, in our custom code, we should use the CloseableHttpClient class, not the HttpClient interface.

HttpClients is a utility class containing factory methods for creating CloseableHttpClient instances:
```
CloseableHttpClient httpClient = HttpClients.createDefault();
```
We can achieve the same using the HttpClientBuilder class. HttpClientBuilder is an implementation of the Builder design pattern for creating CloseableHttpClient instances:
```
CloseableHttpClient httpClient = HttpClientBuilder.create().build();
```
