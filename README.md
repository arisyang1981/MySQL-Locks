# MySQL-Locks

# Metadata locking 
References: \
https://dev.mysql.com/doc/refman/8.0/en/metadata-locking.html 
https://dev.mysql.com/doc/refman/8.0/en/metadata-locking.html \
https://support.oracle.com/epmos/faces/SearchDocDisplay?_adf.ctrl-state=h8du9c63x_4&_afrLoop=300667063032591#GOAL \
Core concepts: \
1 Metadata lock is not a specific engine realtead lock, a MySQL lock. \
2 All objects, not only tables, but aslo schema, routines... \
3 When metadata lock happens: \
Session1: \
START TRANSACTION; \
SELECT * FROM t; \
SELECT * FROM nt; \
Session1 holds metadata locks on both t and nt until the transaction ends. \
Session2 attempts a DDL or write lock operation on either table, it blocks until metadata lock release at transaction end(until session1 commit or rollback). \
DROP TABLE t; \
ALTER TABLE t ...; \
DROP TABLE nt; \
ALTER TABLE nt ...; \
LOCK TABLE t ... WRITE; \
4 Related system tables: \
performance_schema.set_instrucments, performance_schema.metadata_locks, performance_schema.events_statement_concurrent, information_schema.innodb_trx, infodbmaterion_schema.processlist, information_schema.threads. \
5 Fucntions and variables: \
select sys.ps_thread_id(connection())--get the thread id of a connection \
set @@global.lock_wait_timeout=value \
set @@session.lock_wait_timeout=vale \
6 How to avoid:
Use online schema tool to deploy DDL \
Avoid expictly transaction mode, for example, in Java, 'set @@session.autocommit=1', avoid 'start transaction', and commit transaction in time. \ 




