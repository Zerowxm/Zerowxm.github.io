---
layout: post
title: How to Implement HashTable in Java
key: 20180130
tags: Java HashTable
---

# What is HashTable
[HashTable](https://en.wikipedia.org/wiki/Hash_table) is a data structure which implements an associative array abstract data type, a structure that can map keys to values. A hash table uses a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

Yesteday, I had a small interview from Intuit, I met with a question, how can I implement hashtable in Java? The first thing came into my brain is array. But I failed to say the detals. So now I search for materials and know it.

# Implementation of HashTable
Here is the API
`public class Hashtable<K,V> extends Dictionary<K,V> implements Map<K,V>, Cloneable, Serializable  `
The important points about Java Hashtable class are:
1.A Hashtable is an array of list. Each list is known as a bucket. The position of bucket is identified by calling the hashcode() method. A Hashtable contains values based on the key.
2.It contains only unique elements.
3.It may have not have any null key or value.
4.It is synchronized.

```java
public class HashTable{
	private static int INITIAL_SIZE = 500;
	private LinkedList<String>[] hashtable = (LinkedList<String>[])new LinkedList[INITIAL_SIZE];
     
    public void add(String value) {
        int hash = hash(value);
        if (hashtable[hash] == null) {
            hashtable[hash] = new LinkedList<>();
        }
        LinkedList<String> bucket = hashtable[hash];
        bucket.add(value);
    }
     
    public boolean contains(String value) {
        int hash = hash(value);
        LinkedList<String> bucket = hashtable[hash];
        if (bucket != null) {
            Iterator<String> it = bucket.iterator();
            while (it.hasNext()) {
                if (it.next().equals(value)) {
                    return true;
                }
            }
        }
        // value not found
        return false;
    }
 
    // exactly the same as contains() just additionally remove value
    public boolean remove(String value) {
        int hash = hash(value);
        LinkedList<String> bucket = hashtable[hash];
        if (bucket != null) {
            Iterator<String> it = bucket.iterator();
            while (it.hasNext()) {
                if (it.next().equals(value)) {
                    it.remove();
                    return true;
                }
            }
        }
        // value not found
        return false;
    }
     
    // use guave library for hash function
    private int hash(String value) {
           value.hashCode() % INITIAL_SIZE;
    }
}
}
```
In oder to make hashTable more effective, every objects should have unique hashCode, because hashtable will first compare hashcode of objects, then use equal of objects, last is reference.
In this simple implementation, the size is fixed, and if several objects have the same key, find or remove an object will consume O(length of linkedList), because key is equal, it would be a linkedlist.

