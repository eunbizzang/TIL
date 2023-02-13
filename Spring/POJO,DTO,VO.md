https://stackoverflow.com/questions/1612334/difference-between-dto-vo-pojo-javabeans
https://kathir-i.medium.com/difference-between-javabeans-vo-pojo-and-dto-e0abc42615f0

VO
- A Value Object or VO is an object such as java.lang.Integer that hold values.
- A value Object is a small object such as a Money or date range object. Their key property is that they follow value semantics rather than reference semantics.
- Value objects should be entirely immutable. If you want to change a value object you should replace the object with a new one and not be allowed to update the values of the value object itself.


DTO
- Data transfer object (DTO), formerly known as value objects or VO, is a design pattern used to transfer data between software application subsystems.
- DTOs are often used in conjunction with data access objects to retrieve data from a database.
- A DTO does not have any logic or behaviour except for the storage and retrieval of its own data.
