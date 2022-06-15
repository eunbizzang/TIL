The @Idannotation is inherited from javax.persistence.Id， indicating the member field below is the primary key of current entity. Hence your Hibernate and spring framework as well as you can do some reflect works based on this annotation. 

The @GeneratedValue annotation is to configure the way of increment of the specified column(field). 
For example when using Mysql, you may specify auto_increment in the definition of table to make it self-incremental, 
and then use 
```
@GeneratedValue(strategy = GenerationType.IDENTITY)
```
 in the Java code to denote 
that you also acknowledged to use this database server side strategy. 
Also, you may change the value in this annotation to fit different requirements.