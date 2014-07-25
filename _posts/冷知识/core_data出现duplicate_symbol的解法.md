# Core Data出现duplicate symbol的解法  
Date: 2013-08-01 21:09  
Tags: 冷知识,iOS,Core Data,duplicate symbol  

是因为一个'NSManagedObject'的subclass中import了另一'NSManagedObject' subclass，不要这么import就OK了~