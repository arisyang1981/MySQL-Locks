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
Session2 attempts a DDL or write lock operation on either table, it blocks until metadata lock release at transaction end. \
DROP TABLE t; \
ALTER TABLE t ...; \
DROP TABLE nt; \
ALTER TABLE nt ...; \
LOCK TABLE t ... WRITE; \




