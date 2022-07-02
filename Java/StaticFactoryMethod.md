https://stackoverflow.com/questions/929021/what-are-static-factory-methods


Factory Method: "Define an interface for creating an object, but let the classes which implement the interface decide which class to instantiate. The Factory method lets a class defer instantiation to subclasses" (c) GoF.


"Static factory method is simply a static method that returns an instance of a class." 


The difference:

The key idea of static factory method is to gain control over object creation and delegate it from constructor to static method. The decision of object to be created is like in Abstract Factory made outside the method (in common case, but not always). While the key (!) idea of Factory Method is to delegate decision of what instance of class to create inside Factory Method. E.g. classic Singleton implementation is a special case of static factory method. Example of commonly used static factory methods:

valueOf
getInstance
newInstance


We avoid providing direct access to database connections because they're resource intensive. So we use a static factory method getDbConnection that creates a connection if we're below the limit. Otherwise, it tries to provide a "spare" connection, failing with an exception if there are none.


```
public class DbConnection{
   private static final int MAX_CONNS = 100;
   private static int totalConnections = 0;

   private static Set<DbConnection> availableConnections = new HashSet<DbConnection>();

   private DbConnection(){
     // ...
     totalConnections++;
   }

   public static DbConnection getDbConnection(){

     if(totalConnections < MAX_CONNS){
       return new DbConnection();

     }else if(availableConnections.size() > 0){
         DbConnection dbc = availableConnections.iterator().next();
         availableConnections.remove(dbc);
         return dbc;

     }else {
         throw new NoDbConnections();
     }
   }

   public static void returnDbConnection(DbConnection dbc){
     availableConnections.add(dbc);
     //...
   }
}
```