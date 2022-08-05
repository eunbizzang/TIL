POST

* GET

/api/posts 200(OK)
: Get all posts

* GET

/api/posts/{id} 200(OK)
: Get post by Id

* POST

/api/posts 201(Created)
: Create a new post

* PUT

/api/posts/{id} 200(OK)
: Update existing post with Id

* DELETE

/api/posts/{id} 200(OK)
: Delete post by Id

* GET

/api/posts?pageSize=5&pageNo=1&sortBy=firstName 200(OK)
: Paginating and sorting posts

---

COMMENT

* GET

/api/posts/{postId}/comments 200(OK)
: Get all comments which belongs to post with id = postId

* GET

/api/posts/{postId}/comments/{id} 200(OK)
: Get comment by id if it belongs to post with id = postId

* POST

/api/posts/{postId}/comments 201(Created)
: Create new comment for post with id = postId

* PUT

/api/posts/{postId}/comments/{id} 200(OK)
: Update comment by id if it belongs to post with id = postId

* DELETE

/api/posts/{postId}/comments/{id} 200(OK)
: Delete comment by id if it belongs to post with id = postId



