
```Pagination.java
@Data
public class Pagination {

    private int pageSize = 10;
    private int blockSize = 10;
    private int page = 1;
    private int block = 1;
    private int totalListCnt;
    private int totalPageCnt;
    private int totalBlockCnt;
    private int startPage = 1;
    private int endPage = 1;
    private int startIndex = 0;
    private int prevBlock;
    private int nextBlock;

    public Pagination(int totalListCnt, int page) {

        setPage(page);
        setTotalListCnt(totalListCnt);
        setTotalPageCnt((int) Math.ceil(totalListCnt * 1.0 / pageSize));
        setTotalBlockCnt((int) Math.ceil(totalPageCnt * 1.0 / blockSize));
        setBlock((int) Math.ceil((page * 1.0)/blockSize));
        setStartPage((block - 1) * blockSize + 1);
        setEndPage(startPage + blockSize - 1);

        if(endPage > totalPageCnt){this.endPage = totalPageCnt;}

        setPrevBlock((block * blockSize) - blockSize);

        if(prevBlock < 1) {this.prevBlock = 1;}

        setNextBlock((block * blockSize) + 1);

        if(nextBlock > totalPageCnt) {nextBlock = totalPageCnt;}

        setStartIndex((page-1) * pageSize);
    }
}
```


```SampleController.java

@RequestMapping(value="/sample", method=RequestMethod.Get)
public ModelAndView sampleList(@RequestParam(defaultValue="1") int page) {
        
        int totalListCnt = sampleService.Count();

		Pagination pagination = new Pagination(totalListCnt, page);

		int startIndex = pagination.getPage();
		int pageSize = pagination.getPageSize();

		List<SampleVO> sampleList = sampleService.findListPaging(startIndex, pageSize);

		ModelAndView mav = new ModelAndView();
		mav.addObject("list", sampleList);
		mav.addObject("pagination", pagination);

        mav.setViewName("thymeleaf/sample/list");
		return mav;
    }
```


```Mapper.java

	<select id="getList" resultType="SampleVO">
        <![CDATA[
		SELECT *
		FROM
			(
				/*index hint*/
				SELECT /*+ INDEX(SAMPLE SAMPLE_PK) */
					ROWNUM R,
					SAMPLE_ID,
					CONTENT,
					REGIST_ID,
					REGIST_DT,
					MODIFY_DT
				FROM SAMPLE
				WHERE ROWNUM <= #{startIndex} * #{pageSize}
			)
		WHERE R> (#{startIndex}-1) * #{pageSize}
		]]>
    </select>

    <select id="Count" resultType="int">
		SELECT count(*) FROM
			SAMPLE
	</select>

```


```samle.html
<nav aria-label="Page navigation example ">
        <ul class="pagination">
            <li class="page-item">
                <a class="page-link" th:href="@{/sample/list?page=1}" aria-label="Previous">
                    <span aria-hidden="true">처음</span>
                </a>
            </li>
            <li class="page-item">
                <a class="page-link" th:href="@{/sample/list?page={page} (page = ${pagination.prevBlock})}" aria-label="Previous">
                    <span aria-hidden="true">이전</span>
                </a>
            </li>
            <th:block  th:with="start = ${pagination.startPage}, end = ${pagination.endPage}">
                <li class="page-item"
                    th:with="start = ${pagination.startPage}, end = ${pagination.endPage}"
                    th:each="pageButton : ${#numbers.sequence(start, end)}">
                    <a class="page-link" th:href="@{/sample/list?page={page} (page = ${pageButton})}" th:text=${pageButton}></a>
                </li>
            </th:block>
            <li class="page-item">
                <a class="page-link" th:href="@{/sample/list?page={page} (page = ${pagination.nextBlock})}" aria-label="Next">
                    <span aria-hidden="true">다음</span>
                </a>
            </li>
            <li class="page-item">
                <a class="page-link" th:href="@{/sample/list?page={page} (page = ${pagination.totalPageCnt})}" aria-label="Previous">
                    <span aria-hidden="true">끝</span>
                </a>
            </li>
        </ul>
    </nav>
```

