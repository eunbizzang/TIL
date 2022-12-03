Beautiful
https://frontbackend.com/thymeleaf/spring-boot-bootstrap-thymeleaf-pagination-jpa-liquibase-h2




JPA Bootstrap

```
@GetMapping("/list")
public ModelAndView methodName(@RequestParam(defaultValue = "0") Integer page, 
                                @RequestParam(defaultValue = "10") Integer pageSize,
                                @RequestParam(defaultValue = "id") String sortBy) {
        ModelAndView modelAndView = new ModelAndView("list");
        Page<exampleListDTO> exampleList = Service.findALL(page, pageSize, sortBy);
        modelAndView.addObject("list",exampleList);
```


```ex.html
<nav class="mt-3 mb-1" aria-label="Page navigation example">
    <ul class="pagination pagination-sm justify-content-center"
    th:with="start=${T(Math).floor(list.number/10)*10 + 1},
    last=(${start + 9 < list.totalPages ? start + 9 : list.totalPages})">

    <th:block th:with=" firstAddr=@{/list(page=0)},
    prevAddr=@{/list(page=${list.number} - 1)},
    nextAddr=@{/list(page=${list.number} + 1)},
    lastAddr=@{/list(page=${list.totalPages} - 1)}">

    <li class="page-item" th:classappend ="${list.first} ? 'disabled'">
        <a class="page-link" th:href="${firstAddr}" aria-label="First">
            <span>&laquo;</span>
        </a>
     </li>
    <li class="page-item" th:classappend ="${list.first} ? 'disabled'">
        <a class="page-link" th:href="${prevAddr}" aria-label="Previous">
            <span>&lt;</span>
        </a>
    </li>
    <li class="page-item" th:each="page : ${#numbers.sequence(start, last)}"
    th:classappend="${page == list.number + 1} ? 'active'">
        <a class="page-link" th:text="${page}" th:href="@{/list(page=${page}-1)}"></a>
    </li>
    <li class="page-item" th:classappend ="${list.last} ? 'disabled'">
        <a class="page-link" th:href="${nextAddr}" aria-label="Next">
            <span aria-hidden="true">&gt;</span>
        </a>
    </li>
    <li class="page-item"  th:classappend ="${list.last} ? 'disabled'">
        <a class="page-link" th:href="${lastAddr}" aria-label="Last">
            <span aria-hidden="true">&raquo;</span>
        </a>
    </li>
    </th:block>
    </ul>
</nav>
```
