## Difference Between Normalization and Denormalization

[site](https://techdifferences.com/difference-between-normalization-and-denormalization.html)

Normalization and denormalization are the methods used in databases. The terms are differentiable where Normalization is a technique of minimizing the insertion, deletion and update anomalies through eliminating the redundant data. 

On the other hand, Denormalization is the inverse process of normalization where the redundancy is added to the data to improve the performance of the specific application and data integrity.

Normalization prevents the disk space wastage by minimizing or eliminating the redundancy.

- comparision chart

|BASIS FOR COMPARISON|NORMALIZATION|DENORMALIZATION|
|:-|-|-:|
|Basic|Normalization is the process of creating a set schema to store non-redundant and consistent data.|Denormalization is the process of combining the data so that it can be queried speedily.|
|Purpose|To reduce the data redundancy and inconsistency.|To achieve the faster execution of the queries through introducing redundancy.|
|Used in|OLTP system, where the emphasize is on making the insert, delete and update anomalies faster and storing the quality data.|OLAP system, where the emphasis is on making the search and analysis faster.|
|Data integrity|Maintained|	May not retain|
|Redundancy|Eliminated|Added|
|# of tables|Increases|decreases|
|Disk space|Optimized usage|Wastage|