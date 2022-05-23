# SortedSet

---

?> Redis的Sorted Set与[Set](/repository/Databases/NoSQL/Redis/docs/Set/README.md)很类似, 都是无相同元素的字符串集合, 不同点在于, Sorted Set 中存储的每个元素都会关联一个评分, Sorted Set就是利用这个评分对其中存储的数据进行顺序的维护, 数据会按照评分保持从低到高的顺序进行排列, 因为元素是不允许重复的, 因此评分也是不会重复的.
