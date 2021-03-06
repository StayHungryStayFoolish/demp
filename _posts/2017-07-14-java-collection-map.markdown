---
layout:     post
title:      "Java 集合框架之 -- Map"
subtitle:   "Map 映射"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-14
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - HashMap
    - LinedHashMap
    - Hashtable
    - TreeMap
---

### Map 映射

- Map 是一个`接口`，使用 Key - Value 键值对存储数据。相当于小型数据库。

- key 具有唯一性

- key -> value 正向，不可逆向，一个键只能映射一个值

- 不同于 Collection 接口添加元素的方法（add 操作），Map 统一使用 put（K，V）

    - put(K,V) 可以`覆盖原有值`

### Map 接口主要实现类

### HashMap 特性

- `无序`

- key，value 不能为 `null`

- 效率高

### Hashtable 特性

- `无序`

- key，value 不能为 `null`

- 初始容量是 `11`，（不同于 Collection 的初始化容量）加载因子0.75

  - `HashMap` `HashSet` `LinkedHashMap` 都是 `16`

- 同步，多线程是安全的。

### LinkedHashMap 特性

- 按`元素添加顺序`排序

- 底层使用 Hashtable 实现

- key，value 不能为 `null`

### TreeMap 特性

- 使用 红 - 黑 树结构存储元素

- 因为基于 NavigableMap 实现，所以按照`键的自然顺序`排序

- 一般用于单线程中，存储有序的映射。

###  方法介绍

- Map 方法

  - clear()

  - containsKey(Object key) 是否包含指定 `键`，无则返回 false

  - containsValue(Object vale) 是否包含一个或多个指定 `值`，无则返回 false

  - entrySet() 返回映射关系视图，使用 Set 来接收

  - equals()

  - get(Object key) 通过指定`键`获取`值`，返回的是 value

  - isEmpty()

  - keySet() 返回键的映射视图，使用 Set 来接收

  - put(K key，V value)

  - putAll(Map<? extends ,? extends V> m) 将指定 Map 放入当前 Map

  - remove(Object key)移除指定键

  - size()

  - values() 返回值得 Collection 视图，使用 `Collection` 接收

- HashMap 实现于 Map，拥有全部方法

- HashTable 实现于 Map，拥有全部方法

- LinkedHashMap 实现于 Map，拥有全部方法

- TreeMap 实现于 Map，拥有全部方法

    - firstEntry() 返回最小键关联的 K - V 映射关系，如果映射为空，返回 null ，使用 Map.Entry() 接收

    - firstKey() 返回第一个（也是最低的） 键

    - floorEntry(K key) 返回小于指定键最大的键-值映射关系，不存在返回 null，使用 Mpa.Entry() 接收

    - floorKey(K key) 返回小于指定键最大的关联键，不存在返回 null

    - lastKey() 返回最后一个（也是最高的）键

    - lowerKey(K key) 返回小于支顶尖的最大键

    - subMap(Key fromKey ,Key toKey) 返回映射视图`左开右闭`


### 例：

- Map 两种遍历


        public class MapDemo{
        	public static void main(String []args){
        		Map<String,String> map = new HashMap<String,String>();
        		map.put("01","lzl-1");
        		map.put("02","lzl-2");
        		map.put("03","lzl-3");
        		map.put("04","lzl-4");
        		map.put("05","lzl-4");
        		method_keySet(map);
        		method_entrySet(map);
        	}
        	public static void method_keySet(Map<String,String> map){
        		//通过keySet方法获取Set<key>类型的值。
        		Set<String> keySet = map.keySet();
        		//有了Set集合，就可以用到Iterator(迭代器)了
        		Iterator<String> it = keySet.iterator();
        		while(it.hasNext()){
        			//获取map集合中的key值
        			String key = it.next();
        			//通过Map集合中的get方法，获取Value值
        			String value = map.get(key);
        			System.out.println("keySet方法--->"+" key:"+key+" value："+value);
        		}
        	}
        	/*

        	*/
        	public static void method_entrySet(Map<String,String> map){
        		//通过entrySet方法获取Map集合中的映射关系
        		Set<Map.Entry<String,String>> entrySet = map.entrySet();
        		//获取Set集合，使用迭代器提供的方法获取Map集合中存入的键值
        		Iterator<Map.Entry<String,String>> it = entrySet.iterator();
        		while(it.hasNext()){
        			//Entry是Map接口这种的内部静态接口，实现该接口的方法，都拥有getValue()和getKey()的方法。
        			Map.Entry<String,String> me = it.next();
        			String value = me.getValue();
        			String key = me.getKey();
        			System.out.println("entrySet方法--->"+" key:"+key+" value："+value);
        		}
        	}
        }

### 一个学生对象，包括姓名和年龄。每个学生都有家庭住址。

- 我们认为学生的姓名和年龄相同表示同一个人。地址可以相同

  步骤：

  1、定义一个学生类，重写hashCode和equals方法。
  并实现Comparable接口，重写compareTo(Object o1,Object o2)方法按照年龄和姓名的顺序来排列

  2、将学生对象和学生的住址存入到HashMap中去。key--Student,value--String(地址)

  3、通过keySet或者entrySet方法将数据一一取出。

  解释：

  因为HashMap底层是hash表，每次new一个对象时，会产生不同的hashCode。因此不能比较Student中姓名和年龄相同的值。
  所以需要覆写hashCode和equals方法
  实现Comparable接口，为了规范，可以使TreeMap集合存储Student对象的数据。若不实现，则不能用TreeMap存储。


            //实现Comparable接口，提供按照姓名和年龄的自然顺序排序的方法
            class Student implements Comparable<Student>
            {
            	private String name;
            	private int age;
            	public Student(String name,int age){
            		this.name = name;
            		this.age = age;
            	}
            	public int getAge(){
            		return age;
            	}
            	public String getName(){
            		return name;
            	}
            	public int compareTo(Student s){
            		int num = this.getName().compareTo(s.getName());
            		if(num == 0)
            			return new Integer(this.getAge()).compareTo(new Integer(s.getAge()));
            		return num;
            	}
            	public int hashCode(){
            		//保证new出的对象的hash值的唯一性
            		return name.hashCode()+age*60;
            	}
            	public boolean equals(Object obj){
            		if(!(obj instanceof Student))
            			throw new RuntimeException("类型不匹配");
            		Student stu = (Student)obj;
            		return this.age==stu.getAge() && this.name.equals(stu.getName());
            	}
            	public String toString(){
            		return "[name = "+name+" age = "+age+"]";
            	}
            }
            public class HashMapDemo{
            	public static void main(String args[]){
            		Map<Student,String> map = new HashMap<Student,String>();
            		map.put(new Student("lzl",18),"河南理工");
            		map.put(new Student("lzl1",18),"河南理工");
            		map.put(new Student("lzl2",18),"河南理工");
            		map.put(new Student("lzl3",18),"河南理工");
            		map.put(new Student("lzl4",18),"河南理工");
            		map.put(new Student("lzl4",18),"河南理工");
            		getInfo(map);
            	}
            	public static void getInfo(Map<Student,String> map){
            		Set<Map.Entry<Student,String>> entrySet = map.entrySet();
            		Iterator<Map.Entry<Student,String>> it = entrySet.iterator();
            		while(it.hasNext()){
            			Map.Entry<Student,String> me = it.next();
            			Student stu = me.getKey();
            			String address = me.getValue();
            			System.out.println("Student:"+stu+" address:"+address);
            		}
            	}
            }