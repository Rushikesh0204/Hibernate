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
 this by <H4>using some boilerplate code which takes each of these properties takes each of the values of the member variables
 and maps it to sequel queries</H> now this mapping is what is a pain I need to convert each object into a sequel query and for
 saving and then for retrieving I'll have to convert a record set into an object and I need to do this for each and 
 every object say I have another class here there would be another table and I will have to do the conversion every time
 
