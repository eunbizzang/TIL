https://www.baeldung.com/spring-jpa-soft-delete

Sometiems there are business requirements to not permanently delete data from db.
for example, the need for data history tracking or audit and also related to reference integrity.


Soft delete performs an update process to mark some data as deleted instead of physically deleting it from a table in the database.


```
// physically deleting a record from the table : 
delete from table_product where id=1
// soft delete
update from table_product set deleted=1 where id=1
```

```
@Entity
@Table(name = "table_product")
@SQLDelete(sql = "UPDATE table_product SET deleted = true WHERE id=?")
@Where(clause = "deleted=false")
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    private double price;

    private boolean deleted = Boolean.FALSE;

    // setter getter methods
}
```

@SQLDelete
: to override the delete command.


@Where
: add a filter when we read the data.(data without the value "deleted = true")


* How to Get the Deleted Data?
```
@Entity
@Table(name = "tbl_products")
@SQLDelete(sql = "UPDATE tbl_products SET deleted = true WHERE id=?")
@FilterDef(name = "deletedProductFilter", parameters = @ParamDef(name = "isDeleted", type = "boolean"))
@Filter(name = "deletedProductFilter", condition = "deleted = :isDeleted")
public class Product {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    private double price;

    private boolean deleted = Boolean.FALSE;
}
```
@FilterDef annotation defines the basic requirements that will be used by @Filter annotation.

Also, we also need to change the Service layer function to handle dynamic parameters or filters.
```
Service
public class ProductService {
    
    @Autowired
    private ProductRepository productRepository;

    @Autowired
    private EntityManager entityManager;

    public Product create(Product product) {
        return productRepository.save(product);
    }

    public void remove(Long id){
        productRepository.deleteById(id);
    }

    public Iterable<Product> findAll(<strong>boolean isDeleted</strong>){
       <strong> Session session = entityManager.unwrap(Session.class);
        Filter filter = session.enableFilter("deletedProductFilter");
        filter.setParameter("isDeleted", isDeleted);
        Iterable<Product> products =  productRepository.findAll();
        session.disableFilter("deletedProductFilter");
        return products;</strong>
    }
}
```

Date타입으로 deleted 설정할 때 처리방식 확인하기