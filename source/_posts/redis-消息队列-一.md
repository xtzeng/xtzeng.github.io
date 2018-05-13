---
title: redis 消息队列(一)
date: 2018-05-13 23:33:43
tags: [redis]
---


Redis队列功能介绍

List

常用命令：

Blpop删除，并获得该列表中的第一元素，或阻塞，直到有一个可用

Brpop删除，并获得该列表中的最后一个元素，或阻塞，直到有一个可用

Brpoplpush

Lindex获取一个元素，通过其索引列表

Linsert在列表中的另一个元素之前或之后插入一个元素

Llen获得队列(List)的长度

Lpop从队列的左边出队一个元素

Lpush从队列的左边入队一个或多个元素

Lpushx当队列存在时，从队到左边入队一个元素

Lrange从列表中获取指定返回的元素

Lrem从列表中删除元素

Lset设置队列里面一个元素的值

Ltrim修剪到指定范围内的清单

Rpop从队列的右边出队一个元素

Rpoplpush删除列表中的最后一个元素，将其追加到另一个列表

Rpush从队列的右边入队一个元素

Rpushx从队列的右边入队一个元素，仅队列存在时有效



   应用场景：

Redis list的应用场景非常多，也是Redis最重要的数据结构之一，比如twitter的关注列表，粉丝列表等都可以用Redis的list结构来实现。

Lists 就是链表，相信略有数据结构知识的人都应该能理解其结构。使用Lists结构，我们可以轻松地实现最新消息排行等功能。

Lists的另一个应用就是消息队列，

可以利用Lists的PUSH操作，将任务存在Lists中，然后工作线程再用POP操作将任务取出进行执行。Redis还提供了操作Lists中某一段的api，你可以直接查询，删除Lists中某一段的元素。

 

如果需要还可以用redis的Sorted-Sets数据结构来做优先队列.可以给每条消息加上一个唯一的序号。这里就不详细介绍了。


示意图:

1)入队

![redis-queue](http://oncykm32h.bkt.clouddn.com/041122275024610.png)


2)jedis rpoplpush

具体方法为



	  /**
	   * Atomically return and remove the last (tail) element of the srckey list, and push the element
	   * as the first (head) element of the dstkey list. For example if the source list contains the
	   * elements "a","b","c" and the destination list contains the elements "foo","bar" after an
	   * RPOPLPUSH command the content of the two lists will be "a","b" and "c","foo","bar".
	   * <p>
	   * If the key does not exist or the list is already empty the special value 'nil' is returned. If
	   * the srckey and dstkey are the same the operation is equivalent to removing the last element
	   * from the list and pusing it as first element of the list, so it's a "list rotation" command.
	   * <p>
	   * Time complexity: O(1)
	   * @param srckey
	   * @param dstkey
	   * @return Bulk reply
	   */

		public String rpoplpush(final String srckey, final String dstkey)

RPOPLPUSH source destination

命令 RPOPLPUSH 在一个原子时间内，执行以下两个动作：

将列表 source 中的最后一个元素(尾元素)弹出，并返回给客户端。
将 source 弹出的元素插入到列表 destination ，作为 destination 列表的的头元素。
举个例子，你有两个列表 source 和 destination ， source 列表有元素 a, b, c ， destination 列表有元素 x, y, z ，执行 RPOPLPUSH source destination 之后， source 列表包含元素 a, b ， destination 列表包含元素 c, x, y, z ，并且元素 c 会被返回给客户端。

如果 source 不存在，值 nil 被返回，并且不执行其他动作。

如果 source 和 destination 相同，则列表中的表尾元素被移动到表头，并返回该元素，可以把这种特殊情况视作列表的旋转(rotation)操作


3） jedis rpop

返回字符串，最后一个元素的值，或者关键不存在返回nil。

	 /**
	   * Atomically return and remove the first (LPOP) or last (RPOP) element of the list. For example
	   * if the list contains the elements "a","b","c" RPOP will return "c" and the list will become
	   * "a","b".
	   * <p>
	   * If the key does not exist or the list is already empty the special value 'nil' is returned.
	   * @see #lpop(String)
	   * @param key
	   * @return Bulk reply
	   */
	
	public String rpop(final String key)

4) jedis lpush

	 /**
	   * Add the string value to the head (LPUSH) or tail (RPUSH) of the list stored at key. If the key
	   * does not exist an empty list is created just before the append operation. If the key exists but
	   * is not a List an error is returned.
	   * <p>
	   * Time complexity: O(1)
	   * @param key
	   * @param strings
	   * @return Integer reply, specifically, the number of elements inside the list after the push
	   *         operation.
	   */
	
	 public Long lpush(final String key, final String... strings)