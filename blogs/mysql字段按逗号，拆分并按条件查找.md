# mysql字段按逗号，拆分并按条件查找
## mysql 表结构
```
CREATE TABLE `subid` (
  `id1` varchar(255) DEFAULT NULL,
  `id2` varchar(255) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

INSERT INTO `mysql`.`subid`(`id1`, `id2`) VALUES ('1,2,3', 'A,G,H');
INSERT INTO `mysql`.`subid`(`id1`, `id2`) VALUES ('2,3,4', 'D,F,G');
INSERT INTO `mysql`.`subid`(`id1`, `id2`) VALUES ('1,4,5', 'H,L,K');
INSERT INTO `mysql`.`subid`(`id1`, `id2`) VALUES ('1,3,2', 'gg,uu,kk');

```
## 查找2所对应的值
```
SELECT
	idone,
	idtwo 
FROM
	(
SELECT
	substring_index( substring_index( t.id1, ',', b.help_topic_id + 1 ), ',', - 1 ) AS idone,
	substring_index( substring_index( t.id2, ',', b.help_topic_id + 1 ), ',', - 1 ) AS idtwo 
FROM
	subid t
	JOIN mysql.help_topic b ON b.help_topic_id < ( LENGTH( t.id1 ) - LENGTH( REPLACE ( t.id1, ',', '' ) ) + 1 ) 
	) AS allId 
WHERE
	idone = 2
```
## 结果 
![result](https://www.cnblogs.com/images/cnblogs_com/ants_double/1413361/o_2019-06-26%20111923.png)
