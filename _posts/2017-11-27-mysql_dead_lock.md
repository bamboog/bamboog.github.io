---
layout: post
title: mysql_dead_lock
date: 2017-11-27
tags: mysql
---
## log
[25 Nov 10:51] xu wen
Description:
On some conditions , UPDATE query uses index_merge when one key is unique and  another key is index;
eg:

explain  update order_test set last_updated=now() where
order_no = "a8fb22d3cf4c11e7be620" and  last_updated="2018-05-17 14:46:42";

When the same 'last_updated' value, increases chances for deadlock.

How to repeat:
//create table
drop table if exists order_test;
CREATE TABLE `order_test` (
  `id` int  AUTO_INCREMENT PRIMARY KEY,
  `order_no` varchar(32),
  `last_updated` datetime,
  unique `order_no_idx` (`order_no`),
  index `last_update_idx` (`last_updated`)
) engine = innodb;

//insert data
DELIMITER ;;
CREATE PROCEDURE batch_insert()
BEGIN
DECLARE y int DEFAULT 1;
WHILE y<9000000
DO
insert into order_test(order_no,last_updated)  values (replace(uuid(), '-', ''),"2011-05-17 14:46:42.0");
SET y=y+1;
END WHILE ;
commit;
END;;
CALL batch_insert();

//test
explain  update order_test set last_updated=now() where
order_no = "a8fb22d3cf4c11e7be620" and  last_updated="2018-05-17 14:46:42";

`id, select_type, table, type, possible_keys, key, key_len, ref, rows, Extra `
'1', 'SIMPLE', 'order_test', 'index_merge', 'order_no_idx,last_update_idx', 'order_no_idx,last_update_idx', '99,6', NULL, '1', 'Using intersect(order_no_idx,last_update_idx); Using where; Using temporary'

Suggested fix:
When index is unique,use unique replace index_merge;
