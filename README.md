<pre>
WHY Hibernate?
It mediates the applications interaction with a relational database, leaving the developer free to concentrate on the 
business problem at hand.
J2EE developer does not have to use JDBC API & manage data persistence at RDBMS level.
No need to go to Table/Query/Column level.
One has to bootstrap Hibernate framework , create transient(=not yet persistent) POJOs & then rely entirely on Hibernate 
frmwork to manage persistence

** problem that hibernate is trying to solve 
 would have five you they're objects in my memory now let's say I want to save these user data how would I do that 
 I would use a database
 I would have to store all these user objects and the data in those user objects into the database how would I do that 
 I would have a user table and each of these user objects would have data for a particular user and I would save them as rows
 in the table so what will happen is I would have this table like this I would call this the user table and I will have 
 five columns that correspond to the five member variables of this user class so each of this data has to be saved 
 so let's say I have user object number one I would save this as row number one in this table user object number to be saved 
 as row number two so depending on how many objects I need to save I would have so many rows in this table so a 
 class corresponds to a table and an object of the class corresponds to a row in the table so this is something that 
 we have been doing with the years and what we normally do when it comes to a java application as we normally use a JDBC
 connection and we would connect to the database and then we would take this user object let's say I want to persist 
 user object object 1 now I would take this user object and I would pull up all these fields and I would create a 
 sequel query that would do an insert and I would insert it into this database so depending on what the users information is
 those data would go as sequel query and it would do the insert the same way 
 if I need to create the user object I'll have to do a select on this table and once I do a select I would probably get a
 record set now I'll have to pass this record set and pull up all the individual data and I will have to create a
 new user object and I'll have to feed in all the data say I've got user ID one now when this new user ID or have to do a
 user dot set ID and I have to give the value user dot set name I'd have to give the name so depending on what I've gotten 
 in the record set I have to create the object 
 ** so the problem here is this I have objects here in Java but I do not have objects here in the database level this is a 
 individual entity that needs to be converted to this individual entity which is the true and the very normally converted 
 this by <H4> using some boilerplate code which takes each of these properties takes each of the values of the member variables
 and maps it to sequel queries </H> now this mapping is what is a pain I need to convert each object into a sequel query and for
 saving and then for retrieving I'll have to convert a record set into an object and I need to do this for each and 
 every object say I have another class here there would be another table and I will have to do the conversion every time

 The problem
● Mapping member variables to columns
● Mapping relationships
● Handling data types
● Managing changes to object state
Formally referred as -- Object-Relational Impedance Mismatch' (sometimes called the 'paradigm mismatch)
Important Mismatch Points
1. Granularity
2. Sub Types or inheritance n polymorphism 3. Identity
4. Associations
5. Data Navigation
   
Cost of Mismatch
1.SQL queries in Java code
2.Iterating through ResultSet & mapping it to POJOs or entities. 3.SQL Exception handling.
4. Transaction management
5. Caching
6. Connection pooling
7. Boiler plate code

Configuration JDBC Driver
JDBC drivers for that database so what's happening here is that while heaven it provides a layer of abstraction when it
comes to the database connections hibernate internally is using JDBC to connect to the database and depending on what 
database that we using ever we are configuring happening to connect to we will have to supply hibernate with that JDBC 
driver so that it can use that driver to connect to the database

<H3> Saving Without Hibernate </H3>
● JDBC Database configuration 
--> we need to tell JDBC which database we are actually interested in we need to give the you
know the IP the port number and the user ID password so this kind of configuration has to be done for the JDBC to allow it
to connect to the database
● The Model object 
--> model object which is the object that we want to save
● Service method to create the model object
--> some method which provides the values to the object and creates an object in 
● Database design
--> I do before I write code to save I will need to have a table in place in my database which which holds this user object 
so depending on the fields that I want to save I will have to create the tables and have the corresponding columns so that 
I can save the object data into that table
● DAO method to save the object using SQL queries
--> DAO layer we need to write code which is a method which takes this object and it generates the sequel queries it call 
it uses the JDBC connection and it creates a connection it runs the query and it inserts the data to the database

<H3> The Hibernate way </H3>
● JDBC Database configuration - – Hibernate configuration
--> still need to tell that framework what the database is this is done in hibernate by using the hibernate configuration
file it's an XML file that we will write and this will give information to hibernate as to what database it needs to connect
● The Model object – Annotations
--> module object because hibernate needs to know what object it needs to save and we will have a mortal object and we will 
configure it in such a way that hibernate knows what needs to be saved and how
● Service method to create the model object – Use the Hibernate API
--> model object and normally what it would do is it would pass the model object to a data layer which uses C JDBC instead
in the hibernate way of doing things the service method would pass the object to hibernate ap is the method would use
hibernate API statically or pass it on to a data layer which uses hibernate ap is so it's actually the hibernate API 
switch do the save of the model object database design 
● Database design – Not needed!
--> create a table for every object as long as you configure the model object the right way hibernate creates the tables itself
● DAO method to save the object using SQL queries - Not needed!
--> writing data layer code for converting objects into a relational model so this major step is actually not needed when
they using hibernate as I mentioned here the service method directly calls the hibernate api's and the hibernate api's take
care of saving the object 

<H1> XML file </H1> 
<hibernate-configuration>
    <session-factory>
        --> Database connection settings -->
        <property name="connection.driver_class">org.h2.Driver</property>
        <property name="connection.url">jdbc:h2:mem:db1;DB_CLOSE_DELAY=-1;MVCC=TRUE</property>
        <property name="connection.username">sa</property>
        <property name="connection.password"></property>
     
        --> JDBC connection pool (use the built-in) -->
        <property name="connection.pool_size">1</property>
        
        --> SQL dialect --> dialect mean dialect is uh it's a configuration that you specify here so that uh hibernate 
                            knows what kind of language it needs to use to talk to uh the database
                                 class inside the hibernate pkg
        <property name="dialect">org.hibernate.dialect.H2Dialect</property>
        
        --> Disable the second-level cache -->
        <property name="cache.provider_class">org.hibernate.cache.NoCacheProvider</property>
        
        --> Echo all executed SQL to stdout -->
        <property name="show_sql">true</property>
        
        --> Drop and re-create the database schema on startup --> create -->every time create db
                                                                  update --> if present not create db
        <property name="hbm2ddl.auto">create</property>
        
        --> Names the annotated entity class -->mapping class here it says names the annotated entity class so what this 
                                    is doing is uh here we need to list out all the model classes that we have configured
                                    - using this hibernate create table
                                                                         (give some Clues to hibernate as to how to
                                                                          persist this class and the way we do that the
                                                                          way we configure this is by using annotations
                                                                          here we can also configure this using XML 
        <mapping class="org.hibernate.tutorial.annotations.Event" />
        
    </session-factory>
</hibernate-configuration>

</hibernate-configuration>

Some basics
1. Hibernate uses runtime reflection to determine the persistent properties of a class.

2. objects to be persisted(called as POJO or Entity) are defined in a mapping document or marked
with annotations.
Either these HBM XML docs or annotations serves to describe the persistent fields and associations,
as well as any subclasses or proxies of the persistent object.

3.  mapping documents or annotations are compiled at application startup time and provide the
framework with necessary information for a persistent class.

4. What is Hibernate config.?
An instance of Hib Configuration allows the application to specify properties and mapping documents
to be used at the frmwork start-up.
The Configuration : initialization-time object.
         
5. SessionFactory is created from the compiled collection of mapping documents .
   The SessionFactory provides the mechanism for managing persistent classes, the Session interface.
         What is SessionFactory?
-------------------------------
It is a factory(provider) of session objects.
we use sessionfactory object to create session object
It is a heavy weight object, therefore it has to
be created only once for an application(typically @ appln start up time) -- typically one per DB per
web application.
Its immutable --- Once SF is created , changes made to hibernate.cfg.xml will not be auto reflected in SF

6. A web application or Java SE apllication will create a single Configuration, build a single instance of
SessionFactory and then instantiate multiple Sessions in threads servicing client requests.
         
SessionFactory : immutable and does not reflect any changes done later to the Configuration.
         
7. The Session class provides the interface between the persistent data store and the application.
      will create sessions from the session factory and then once you have a session you will use that session the save 
      model objects in this case it is a save it could be any other database operation



  1--> I create a new configuration object and I will call a method of this configuration
  2--> object called configure now what this configure method does is it takes the it takes this configuration file and 
         then it reads the configuration file to understand what is the database configuration that needs to be made 
  3-->we can call the build session factory method now this build session factory method returns a session factory so this 
         is what we need so I will create a new session factory object and I will assign this configuration configure dot 
         build session Factory



    **     SessionFactory sessionFactory = new Configuration ().configure() .buildSessionFactory()
         I am taking the configuration then calling the configure method of the configuration so that you know it goes to
         this XML file and then it reads the configuration and then I'm calling the build session factory so that it
         varies a session factory object based on the configuration that we have provided now the build session factory 
         returns factory object







         
        </pre>
 
