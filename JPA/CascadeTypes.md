Referenced:

https://www.baeldung.com/jpa-cascade-types

https://howtodoinjava.com/hibernate/hibernate-jpa-cascade-types/


Entity relationships often depend on the existence of another entity.
Cascading is the way to achieve this. When we perform some action on the target entity, the same action will be applied to the associated entity.

---
JPA Cascade Type
* ALL
* PERSIST
* MERGE
* REMOVE
* REFRESH
* DETACH
---


 Hibernate Cascade Type

: Hibernate supports three additional Cascade Types along with those specified by JPA.

    * REPLICATE
    * SAVE_UPDATE
    * LOCK
---
Difference Between the Cascade Types
1. CascadeType.ALL


```EmployeeEntity.java
@Entity
@Table(name = "Employee")
public class EmployeeEntity implements Serializable
{
	private static final long serialVersionUID = -1798070786993154676L;
	@Id
	@Column(name = "ID", unique = true, nullable = false)
	private Integer           employeeId;
	@Column(name = "FIRST_NAME", unique = false, nullable = false, length = 100)
	private String            firstName;
	@Column(name = "LAST_NAME", unique = false, nullable = false, length = 100)
	private String            lastName;

	@OneToMany(cascade=CascadeType.ALL, fetch = FetchType.LAZY)
	@JoinColumn(name="EMPLOYEE_ID")
	private Set<AccountEntity> accounts;

	//Getters and Setters Hidden
}
```

```AccountEntity.java
@Entity
@Table(name = "Account")
public class AccountEntity implements Serializable
{
	private static final long serialVersionUID = 1L;
	@Id
	@Column(name = "ID", unique = true, nullable = false)
	@GeneratedValue(strategy = GenerationType.SEQUENCE)
	private Integer           accountId;
	@Column(name = "ACC_NO", unique = false, nullable = false, length = 100)
	private String            accountNumber;

	@ManyToOne (mappedBy="accounts",  fetch = FetchType.LAZY)
	private EmployeeEntity employee;

}
```
EmployeeEntity defines “cascade=CascadeType.ALL” and it essentially means that any change happened on EmployeeEntity must cascade to AccountEntity as well.


Simply If we save an employee, then all associated accounts will also be saved into the database. If you delete an Employee then all accounts associated with that Employee also be deleted.


But if we only want the cascading on save operations but not on delete operation, then we need to clearly specify it using the below code.

```
@OneToMany(cascade=CascadeType.PERSIST, fetch = FetchType.LAZY)
@JoinColumn(name="EMPLOYEE_ID")
private Set<AccountEntity> accounts;
```
Now only when save() or persist() methods are called using Employee instance then the accounts will be also be persisted. 


The cascade configuration option accepts an array of CascadeTypes; thus, to include only refreshes and merges in the cascade operation for a One-to-Many relationship as in our example, we might use the following:

```
@OneToMany(cascade={CascadeType.REFRESH, CascadeType.MERGE}, fetch = FetchType.LAZY)
@JoinColumn(name="EMPLOYEE_ID")
private Set<AccountEntity> accounts;
```
Above cascading will cause accounts collection to be only merged and refreshed.



CascadeType.REMOVE vs Orphan Removal
* The orphanRemoval option was introduced in JPA 2.0. This provides a way to delete orphaned entities from the database.
* While CascadeType.REMOVE is a way to delete a child entity or entities whenever the deletion of its parent happens.

Whenever we delete an employee, all his accounts will get deleted if we use the CascadeType.REMOVE. But if want that whenever we remove the relationship between an account and an employee, hibernate will check for the accounts in other references. If none is found, hibernate will delete the account since it’s an orphan.


https://vladmihalcea.com/orphanremoval-jpa-hibernate/
    JPA and Hibernate orphanRemoval vs. CascadeType.REMOVE
    A very common question is how the orphanRemoval mechanism differs from the CascadeType.REMOVE strategy.

    If the orphanRemoval mechanism allows us to trigger a remove operation on the disassociated child entity, the CascadeType.REMOVE strategy propagates the remove operation from the parent to all the child entities.

    Because the comments collection uses CascadeType.ALL, it means it also inherits the CascadeType.REMOVE strategy.

    ```
    Post post = entityManager.createQuery("""
        select p
        from Post p
        join fetch p.comments
        where p.id = :id
        """, Post.class)
    .setParameter("id", postId)
    .getSingleResult();
    
    entityManager.remove(post);
    ```
    Hibernate is going to execute three DELETE statements:

    ```
    DELETE FROM
        post_comment
    WHERE
        id = 2
    
    DELETE FROM
        post_comment
    WHERE
        id = 3
    
    DELETE FROM
        post
    WHERE
        id = 1
    ```
    First, the child rows are deleted, because if we deleted the post row first, a ConstraintViolationExeption would be triggered since there would be still post_comment rows associated with the post record that was wanted to be deleted.


