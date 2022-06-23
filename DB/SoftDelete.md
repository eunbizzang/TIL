https://stackoverflow.com/questions/2549839/are-soft-deletes-a-good-idea
https://stackoverflow.com/questions/378331/physical-vs-logical-hard-vs-soft-delete-of-database-record
https://blog.sqlauthority.com/2010/09/03/sql-server-soft-delete-isdelete-column-your-opinion/

soft(logical) deletes a good idea or a bad idea? (soft vs hard(physical))



advantages

1. in situations ex) legally required to truly delete something. 

Maybe someone has requested that their social security number be permanently removed from your system. 



disadvantages

1. can't do cascading deletions, which automatically clear out any references to the deleted data to prevent foreign key violations. 

2. those unwanted data will potentially affects the db performance.
-> move all "deleted" items to a backup table instead of leaving them to the current running tables.


* If you're going to use soft deletion, it's a good idea to have a deleted_date field, instead of an is_deleted field

* your database should be backed up regularly, so you should never be in a situation where you would lose data permanently because of a DELETE