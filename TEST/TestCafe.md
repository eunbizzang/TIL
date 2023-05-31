https://efcl.info/2016/10/23/testcafe/
https://blog.coderifleman.com/2016/10/31/good-first-impression-testcafe/
https://blog.recruit.co.jp/rmp/front-end/post-20193/


TestCafe とは、Developer Express Inc. というアメリカのシステム開発会社が開発している E2E テストツールです。


```
import 'testcafe';
import { Selector } from 'testcafe';

// 1.
fixture('Getting started').page('http://devexpress.github.io/testcafe/example');

test('My first test', async (t: TestController) => {
  await t
    .typeText('#developer-name', 'wakamsha') // 2.
    .click('#submit-button') // 3.
    .expect(Selector('#article-header').innerText) // 4-a.
    .eql('Thank you, wakamsha!'); // 4-b.
});
```
