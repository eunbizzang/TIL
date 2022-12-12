https://hongs-coding.tistory.com/125


```Criteria.java
@Data
public class Criteria {

    private int pageNum;
    private int amount;
    private String type;
    private String keyword;

    public Criteria() { this(1, 10); }

    public Criteria(int pageNum, int amount) {
        this.pageNum = pageNum;
        this.amount = amount;
    }

    public String getListLink() {
        UriComponentsBuilder builder = UriComponentsBuilder.fromPath("")
                .queryParam("pageNum", pageNum)
                .queryParam("amount", amount);

        return builder.toUriString();
    }

    public String[] getTypeArr() {
        return type == null ? new String[]{} : type.split("");
    }
}
```


```PageDTO.java
@Data
public class PageDTO {
    private int pageCount;
    private int startPage;
    private int endPage;
    private int realEnd;
    private boolean prev, next;
    private int total;
    private Criteria criteria;

    public PageDTO() {}

    public PageDTO(int pageCount, int total, Criteria criteria) {

        this.total = total;
        this.criteria = criteria;
        this.pageCount = pageCount;

        this.endPage = (int)(Math.ceil(criteria.getPageNum()*1.0/pageCount))*pageCount;
        this.startPage = endPage - (pageCount-1);

        realEnd = (int)(Math.ceil(total*1.0 / criteria.getAmount()));

        if(endPage>realEnd) {
            endPage = realEnd == 0 ? 1 : realEnd;
        }

        prev = startPage > 1;
        next = endPage < realEnd;

    }
}
```

```Mapper.java
<!--    게시글 목록 가져오기-->
	<select id="getList" resultType="DTO">
        <![CDATA[
		SELECT *
		FROM
			(
				/*알리아스를 붙인 컬럼에 WHERE절에서 접근할 때에는 FROM 절에 작성된 테이블의 컬럼과 동일한 이름으로만 사용이 가능하다.*/
				SELECT /*+ INDEX_DESC(TBL_BOARD PK_BOARD) */
                ROWNUM R, BNO, TITLE, CONTENT, WRITER, REGDATE, UPDATEDATE
                FROM TBL_BOARD
                WHERE ROWNUM <= #{pageNum} * #{amount}
			)
		    WHERE R> (#{pageNum}-1) * #{amount}
		]]>

    </select>

```


```DAO
public List<BoardVO> getList(Criteria cri) {
    return mapper.getList(cri);
}
```


```list.html
<div th:object="${pageMaker}">
    <div class="big-width" style="text-align: center">
        <a class="changePage" th:if="*{prev}" th:href="*{startPage - 1}"><code>&lt;</code></a>
        <th:block th:each="num : ${#numbers.sequence(pageMaker.getStartPage(), pageMaker.getEndPage())}">
            <code th:if="${pageMaker.criteria.getPageNum() == num}" th:text="${num}"></code>
            <a class="changePage" th:unless="${pageMaker.criteria.getPageNum() == num}" th:href="${num}"><code th:text="${num}"></code></a>
        </th:block>
        <a class="changePage" th:if="*{next}" th:href="*{endPage + 1}"><code>&gt;</code></a>
    </div>
    <div class="small-width" style="text-align: center">
        <a class="changePage" th:if="*{criteria.pageNum > 1}" th:href="*{criteria.pageNum - 1}"><code>&lt;</code></a>
        <code th:text="*{criteria.pageNum}"></code>
        <a class="changePage" th:if="*{criteria.pageNum < realEnd}" th:href="*{criteria.pageNum + 1}"><code>&gt;</code></a>
    </div>
    <form action="/board/list" th:object="${criteria}" name="pageForm">
        <input type="hidden" name="pageNum" th:field="*{pageNum}">
        <input type="hidden" name="amount" th:field="*{amount}">
    </form>
</div>
```