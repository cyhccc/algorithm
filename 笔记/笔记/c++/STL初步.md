# STL初步

 STL也就是C++标准模板库,它是C++标准库的一部分。

分为两种

* 序列式容器 vector ,list,queue,stack...
* 关联式容器 map,set..

## 序列式容器 

### 不定长数组vector

#### 创建vector容器的几种方式

1. 常规  (**数据类型**可以是结构体，也能是另外一个容器，后文用T表示)

```
vector<数据类型>v
```

2. 创建时，声明大小

```
vector<数据类型>v (size);//size大小
```

3. 声明大小，并且附上初始值。

```
vector<数据类型>v (size,value);//size大小 value初始值 均可以用变量表示
```

4. 创建时，声明初始值(可以类比数组)

```
vector<数据类型>v {1,3,5,7};
```

5. 二维数组

```
vector<?>v;
```

* 二维数组的**练习**（画图讲解

1. 声明10*5固定大小的二维数组

   ```
   vector< vector<int> > v4(10, vector<int>(5)  );
   ```

2. 声明10*5固定大小的二维数组并且都赋值为1

   ```
   vector< vector<int> > v4(10, vector<int>(5,1));
   ```

3. 遍历二维数组

   ```
   	for (int i = 0; i < v4.size(); i++) {
   		//v4[i]是长度为5的数组
   		for (int j = 0; j < v4[i].size(); j++) {
   			cout << v4[i][j];
   		}
   		cout << endl;
   	}
   ```

#### 成员函数

| 函数                 | 作用                                       |
| -------------------- | ------------------------------------------ |
| back()               | 返回最后一个元素的**引用**                 |
| front()              | 返回第一个元素的**引用**                   |
| begin()              | 返回第一个元素的迭代器                     |
| end()                | 返回**最后一个元素**的后一个位置的迭代器   |
| push_back()          | 在序列尾部添加一个元素                     |
| pop_back()           | 移出序列尾部的元素。                       |
| emplace_back()       | vector 容器的尾部添加一个元素。(c++11才有) |
| erase()              | 移除**一个**或**一段**元素，参数是迭代器。 |
| clear()              | 移除所有元素，容器大小为0。                |
| resize()             | 重新改变容器的容量                         |
| size()               | 返回实际元素的个数                         |
| insert(迭代器，元素) | 在迭代器位置插入元素                       |

#### push_back 和 emplace_back 的区别

* push_back：创建元素再搬运
* emplace_back：在末尾直接生成，效率更高，但是只有c++11以后。



#### 用sort 对vector排序(练习)



### 迭代器iterator

迭代器不是指针，是类模板，表现的**像**指针。

是一个可遍历STL容器内全部或部分元素”的对象。

迭代器**只能**指向容器。

总结：只能指向容器的**特殊指针**



* 基本声明方式

```
容器::iterator it = v.begin();
```

* 懒人声明方式

```
auto it =v.begin();
```

* 
* 迭代器遍历容器

	for (vector<int>::iterator i = v.begin(); i != v.end(); i++) {
		cout << *i;
	}
* 懒人遍历容器

```
for (auto i = v.begin(); i != v.end(); i++) {
	cout << *i;
}
```



#### 增强for循环（foreach）c++11

1. 遍历数组

```
for(int i: array){

}
```

2.遍历容器(如：vector\<int>)

```
for(auto i:vector){// auto = vector<int>::iterator 

}
```

### 链表list

#### 创建list容器的几种方式

1. 常规

```
list<数据类型>ls
```

2. 创建时，声明大小

```
list<数据类型>ls (size);//size大小
```

3. 声明大小，并为每个元素指定初始值。

```
list<数据类型>ls (size,value);//size大小 value初始值 均可以用变量表示
```





### 栈stack

### 队列queue







## **关联式**容器

此类容器在存储元素值的同时，还会为各元素额外再配备一个**值**（又称为“**键**”），通常是根据key找到value。

C++ STL 标准库提供了 4 种关联式容器，分别为 map、set、multimap、multiset，

> 除此之外，C++ 11 还新增了 4 种哈希容器，即 unordered_map、unordered_multimap 以及 unordered_set、unordered_multiset。但由于哈希容器底层采用的是哈希表，而不是红黑树，因此分开进行讲解。

### 对组pair

![image-20210309171838688](C:\Users\37802\AppData\Roaming\Typora\typora-user-images\image-20210309171838688.png)

#### 创建pair的几种方式

1. 常规

```
pair<T,T>p;
```

2. 声明时赋值

```
pair <T, T> pair2 (value1,value2); 
```

3. 示例

```
pair<string,string>p("我是第一个","我是第二个");
```

#### 输出pair的值

pair由两部分组成，键first，值second

```
pair<T,T>p;
cout<<p.frist<<" "<<p.second;
```



#### pair重载比较函数(续)

默认重载了内部的比较机制 ，是比较第一个键的大小**升序**，一个键值对相同，就比较第二个键值对。

* 示例

```
vector< pair<int, int> >v;
	pair<int, int> a(1, 2);
	pair<int, int> b(1, 3);
	pair<int, int> c(2, 2);
	v.push_back(a);
	v.push_back(b);
	v.push_back(c);
	sort(v.begin(), v.end());
	for (auto i : v) {
		cout << i.first << " " << i.second << endl;
	}
```

### 集合set

* 集合：没有重复元素

#### 创建set的几种方式

1. 常规

```
set<T>s;
```

2. 声明时初始化

```
set< T >s{value1,value2.....}; 
```

#### set的特性

1. 每次insert的时候，都会自动排好序。（默认升序)
2. 键值对， key 和值 value 相同。

#### 讲解顺序

1. insert

2. 迭代

```
int main() {
	for (set<int>::iterator it=s.begin(); it != s.end(); it++) {
		cout << *it;
	}
```

3. 其他函数
4. 原理(key value 相同 )
5. 修改值出现的问题(   删除  再 )

#### 常用函数

| 函数       | 说明                                                         |
| :--------- | ------------------------------------------------------------ |
| insert()   | 向 set 容器中插入元素。                                      |
| erase()    | 删除 set 容器中存储的元素。                                  |
| empty()    | 若容器为空，则返回 true；否则 false。                        |
| begin()    | 返回指向容器中第一个（排好序的第一个）元素的迭代器           |
| end()      | 返回指向容器最后一个元素（已排好序的最后一个）所在位置后一个位置的双向迭代器 |
| find(val)  | 查找值为 val 的元素的，如果找到放回该元素的迭代器，如果没找到返回end() |
| count(val) | 查找值为 val 的元素的个数，该函数的返回值最大为 1。          |

#### 自定义set排序规则(暂时不讲)

```c++
struct intComp {
	bool operator() (const int& lhs, const int& rhs) const {
		return lhs > rhs;
	}
};	
```
#### multiset

可以重复存在的集合。

用count()读取个数



### 键值对容器map

map 容器存储的都是 pair 对象



#### 创建map的几种方式

1. 常规

```
map<int,int>mp
```

2. 声明时初始化

```c++
	pair<int, int>a1(1,2);
	pair<int, int>a2(3,4);
	pair<int, int>a3(5,6);
	map<int, int>mp{ a1,a2,a3 };
```

#### 常用函数

| 函数      | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| begin()   | 返回指向容器中第一个（是已排好序的第一个）键值对的迭代器     |
| end()     | 返回指向容器最后一个元素（已排好序的最后一个）所在位置后一个位置的迭代器， |
| find(key) | 在 map 容器中查找键为 key 的键值对，如果成功找到，则返回指向该键值对的双向迭代器；反之，则返回和 end() |
| size()    | 返回当前 map 容器中存有键值对的个数。                        |
| empty()   | 若容器为空，则返回 true；否则 false。                        |
| erase()   | 删除 map 容器指定位置、指定键（key）值或者指定区域内的键值对 |
| clear()   | 清空 map 容器中所有的键值对，即使 map 容器的 size() 为 0。   |

#### 下标访问的陷阱

	map<int, int>mp;
	mp[1] = 1;
	mp[2] = 2;
	cout << mp[0] << endl;
	cout << mp.size();
#### 遍历

```
	for (auto i : mp) {
		cout << i.first << " " << i.second << endl;
	}
```























### 双向队列deque

### 优先队列priority_queue



### 常用STL算法

#### sort



#### find

#### lower_bound  upper_bound

在一个**左闭右开**的**有序区间**里进行**二分查找**	

* lower_bound：返回大于等于值的第一个指针
* upper_bound：返回大于值的第一个指针
