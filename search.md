---
title: "Search"
tags: ""
---

# Symbol tables

Function of Symbol Table

-   insert a new pair into table
-   search for the value

## API

public class ST&lt;Key, Value>

-   create a symbol table
        ST()
-   put key-value pair into the table
        void put(Key key, Value, val)	
-   valued paired with key
        Value get(Key key)
-   remove key(and its value from the table
        void delete(Key key)
-   is there a value paired with key?
        boolean contains(Key key)
-   Is the table empty?
        boolean isEmpty()
-   number of pairs
        int size()

### Conventions

-   Values are not null
-   如果table里面没有对应的key,get()以后return null
-   如果table里面已经有key，put()以后新的value代替旧的

#### Shorthand methods

| method                    | default implementation  |
| ------------------------- | ----------------------- |
| void delete (Key key)     | put(key,null)           |
| boolean contains(Key key) | return get(key) != null |
| boolean isEmpty()         | return size() == 0;     |

### ST test For traces

Build ST by associating value i with ith string from standard input

    public static void main(String[] args)
    {
    	ST<String, Integer> st = new ST<String, Integer>();
        for (int i = 0; !StdIn.isEmpty(); i++)
        {
        	String key = StdIn.readString();
            st.put(key, i);
        }
        for (String s: st.keys())
        	StdOut.println(s + ' ' + st.get(s));
        }
    }

### Frequency counter implementation

    public class FrequencyCounter
    {
    	public static void main(String[] args)
        {
        	int minlen = Integer.parseInt(args[0]);
            ST<Sting, Integer> st = new ST<String, Integer>();
            while (!StdIn.isEmpty())
            {
            	String word = StdIn.readString();
                if (word.length() < minlen) continue;
                if(!st.contains(word))	st.put(word.1);
                else		st.put(word, st.get(word) + 1);
            }
        String max = '';
        st.put(max, 0);
        for(String word: st.keys())
        	if (st.get(word) > st.get(max))
            	max = word;
            StdOUt.println( max + " " + st.get(max));
        }
    }

## Elementary implementations

### Sequential search in a linked list

-   Maintain an unordered linked list of key-value pairs

-   Search: 从左到右scan所有的Key直到找到为止

-   Insert:先search一遍，如果找不到在前面加

### Binary search in an unordered array

一分为二，分别查找

    public Value get(Key key)
    {
        if isEmpty()    return null;
        int i = rank(key);
        if(i < N && keys[i].compareTo(key) == 0)    return keys[i];
        else    return null;
        
    }

    private int rank(Key key)
    {
        int lo = 0, hi = N-1;
        ;
        while(lo<=hi)
        {
            int mid = (hi + lo)/2
            int cmp = keys[mid].compareTo(key);
            if(cmp > 0)     hi = mid - 1;
            else if(cmp < 0)    lo = mid + 1;
            else if (cmp == 0)  return mid;
        }
        return lo;
        
    }

### Summary

ST

# Binary search trees

## BSTs

A BST is a binary tree in symmetric order

Symmetric order

-   Every node's key is larger than all keys in the left subtree
-   Every node's key is smaller than all keys in the right subtree

Node 的component

-   key and value
-   reference to the left and right subtree


    private class Node
    {
    	private Key key;
        private Value val;
        private Node left, right;
        public Node (Key key, Value, val)
        {
        	this.key = key;
            that.val = val;
        }
    }

### BST search

-   If less, go left
-   If greater, go right
-   If equal, search hit


    public Value get(Key key)
    {
    	Node x = root;
        while(x != null)
        {
        	int cmp = key.compareTo(x.key);
            if (cmp < 0)	x = x.left;
            else if (cmp > 0)	x = x.right;
            else if (cmp = 0)	return x.value;
        }
        return null;
    }

Cost = 1+ depth of node

### BST insert

Search for key
1\. 如果key 在这个tree里面，reset value
2\. 如果key 不在， add the pairs

    public void put(Key key, Value val)
    {
        put(root, key, val);
    }
    private Node put(Node x, Key key, Value val)
    {
        if (x == null)    return new Node(key, val);
        int cmp = key.compareTo(x.key());
        if(cmp == 0)    x.val = val;
        else if(cmp < 0)    put(x.left, key, val);
        else if (cmp > 0)   put(x.right, key, val);
        return x;
    }

Cost: Number of compares = 1+ depth of node

### Mathematical analysis

Implementation|

## ordered operations

### Maximum and minimum

-   一直往左边找直到null
-   一直往右边找直到null

### floor and ceiling

-   Floor: largest key &lt;= given key
-   Ceiling: Smallest key >= given key

#### Computing the floor

-   k = the key at root

    The foor of k is k
-   k &lt; the key at root

    往左边找
-   k > the key at root

    往右边找，如果如果没有其他数在right subtree 就是此root


    public Key floor(Key key)
    {
        Node x = floor(root, key);
        if x == null    return null;
        else    return x.key;
    }
    private Node floor(Node x, Key key)
    {
        if (x == null)  return null;
        int cmp = key.compareTo(x.key);
        if cmp == 0     return x;
        else if (cmp < 0)      return  floor(x.left, key);
        else if (cmp > 0)
        {
            t = floor(x.right, key);
            if (t = null)   return t;
            else  return x;
        }
    }

### Subtree counts

-   In each node, we store the number of the subtree rooted at the node 
-   当implement size()的时候，return count


    public int size()
    {return size(root)}

    private int size(Node x)
    {
    	if x == null	return 0;
        else	return x.count;
    }

    private node put(Node x, Key key, Value val)
    {
    	if x == null	return new Node(key, val, 1);
        int cmp = key.compareTo(x.key);
        if (cmp < 0)	x.left = put(x.left, key, val);
        else if(cmp > 0)	x.right = put(x.right,key, val)
        else	x.val = val;
        return x;
        x.count = size(x.left) + size(x.right)+ 1;
    }

### Rank

Cases

-   如果key 比x.key小：代入left subtree
-   如果key 比x.key大：left subtree的size加上x本身加上（代入right subtree）的值
-   如果key = x.key： leftsubtree 的size


    public int rank(Key key)
    {
    	return rank(key, root);
    }
    private int rank(Key key, Node x)
    {
    	if (x == null)	return 0;
        int cmp = key.compareTo(x.key);
        if (cmp < 0)	return rank(key, x.left);
        else if(cmp > 0)	return 1 + size(x.left) + rank(key, x.right);
        else if(cmp == 0)	return size(x.left);
    }

### Inorder traversal

-   Traverse left subtree
-   Enqueue key
-   Traverse right subtree


    public Iterable<Key> keys()
    {
    	Queue<key> q = new Queue<key>();
        inorder(root, q);
        return q;
    }
    private void inorder(Node x, Queue<key> q)
    {
    	if (x == null)	return;
        inorder(x.left, q);
        q.enqueue(x.key);
        inorder(x.right, q);
    }

## deletion

### Deleting the minimum

-   Go left until find a node with a null left link
-   Replace that node by its right link
-   Update subtree counts


    public void deleteMin()
    {	return deleteMin(root);}
    private Node deleteMin(Node x)
    {
    	if (x.left == null)	return x.right;
        x.left = deleteMin(x.left);
        x.count = 1 + size(x.left) + size(x.right);
    }

### Hibbord deletion

_TO delete a node with key k: search for node t containing key k_

-   Case 1(0 children): Delete t by setting a parent to null
-   Case 2(1 childre): Delete t by replacing parent link
-   Case 3(2 children)
    -   Find successor x of t(right subtree中最小的）
    -   Delete the min in t's right subtree
    -   put x in t's spot

#### Java implementation

    public void deleteMin(Key key)
    {	return deleteMin(root, key); }
    private Node deleteMin(Node x, Key key)
    {
    	if x == null	return null;
        int cmp = key.compareTo(x.key);
        // Search for key
        if(cmp < 0)		x.left = delete(x.left);		
        else if(cmp > 0)	x.right = delete(x.right);
        else
        {
        	//如果只有一个child, 此node return为那个child
        	if(x.left) == null	return x.right;
            else if(x.right) == null	return x.left;
            else
            {
            	//如果有两个child, 选出right subtree 里的最小值作那个node
            	Node t = x;
                x = min(t.right);
                x.left = t.left;
                x.right = deleteMin(t.right);
                return x;
            }
        }
    }

### Hashcode Caching by String

_aching the hashcode of an object can avoid the recalculation of hashcode again and again and thus increase application performance._

using an object as a key in maps like HashMap.

#### String class's built-in hashcode caching mechanism.

在java 中

the hash code for a String object被计算为

    s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]

-   hashcode depends on its contents

-   object should be immutable

_如果object 是mutable,当内容改变是hashcode 也要改变  _

#### definition of hashCode() method :

      1494       public int hashCode() {
     1495           int h = hash;
     1496           if (h == 0 && count > 0) {
     1497               int off = offset;
     1498               char val[] = value;
     1499               int len = count;
     1500  
     1501               for (int i = 0; i < len; i++) {
     1502                   h = 31*h + val[off++];
     1503               }
     1504               hash = h;
     1505           }
     1506           return h;
     1507       }

-   hash is used to store the haschode for a String object. 

        int h = hash;
-   Definition of hash variable
          122       /** Cache the hash code for the string */
        123       private int hash; // Default to 0
    _each String object's hashcode is stored in this private variable hash._

当hashCode()被调用的时候，

-   检查variable hash 是否为0

-   Variable hash 为0， 意味着 hashcode() method 被第一次调用，未被计算

-   If hash is equals to 0, 只有与string obeject 对应的hash code 被计算，并储存在variable hash中

-   同一个string object的hash code被再次调用时,hash 的值不为0  and hashcode 不会被二次计算，会直接使用hash 里面的值

# Hashing

## Basic plan

Save items in a key-indexed table

-   Hash function
    通过key找到index的方法
-   Issues
    -   Equality test: 检查两个key 是否相等
    -   Collision resolution: 解决两个key hash 到同一个index的情况
-   Classic space-time tradeoff

    在现实情况中，及存在space limitation也存在time limitation，要在两者之间平衡

## Hash function

将keys相对均匀地分配table index中

### Convention

如果x.equal(y) 那么x.hashCode() == y.hashCode()为True， 反之亦然

### Implementing hash code: integers, booleans, and doubles

#### Integer

整数的hash code 是他本身

    public final class Integer
    {
    	private final int value;
        ...
        public int hashCode()
        {	return value;}
    }

#### Boolean

只有正和负，分别return对应的hashcode

    public final class Boolean
    {
    	private final boolean value;
        ...
        public int hashCode()
        {
        	if (value)	return 1231;
            else	return 1237;
        }
    }

#### Doubles

Double 有64bits,hashcode有32bits
先将double 转化为对应的bits,然后Xor most significant 32-bits with least significant 32-bits

    public final class Double
    {
    	private final double value;
        ...
        public int hashCode()
        {
        	long bits = doubleToBits(value);
            return int(bits^(bits >>> 32));
        }
    }

### Implementing hash code: strings

h = s\[0] \* 31^(L-1) +... s\[L-2] \* 31 + s\[L-1] \*31^0

#### Performance optimization

将算好后的hash值h 存储在hash variable 中，下次运算之前检查一下是否之前运算过，如果已经运算过直接调用

    public final class String
    {
        private int hash = 0;
        private char[] s;
        public int hashCode()
        {
            int h = hash;
            if(h != 0)  return h;
            else
            {
                for (int i = 0; i < length(); i++)  
                    h = s[i] + h * 31;
            }
            h = hash;
            return h;
        }
    }

### Modular hashing

-   Hash code: An int between -2^31 and 2^31-1
-   Hash function: an int between 0 and M-1
    先化为正整数在除以约数


    private int hash(Key key)
    {	return(key.hashCode() & 0x7fffffff) % M; }

### Uniform hashing assumption

每个key 都被平均的分配到1~M-1中

## Seperate chaning

### Collision

两个key hash 到同一个index 中
当array 中的元素M小于key的数N

-   Hash: 把key hash 到0~M-1中
-   Insert: 把新添的元素放在第i个chain中
-   Search: 只要找第i 个chain

### Seperate chaining ST: Java Implementation

-   从hashtable 中找某个Key对应的value


    public class SeperateChainingHashST<Key, Value>
    {
    	private int M = 97;		// number of chains
        private Node[] st = new Node[M];
        private static class Node
        {
        	private Object key;
            private Object val;
            private Node next;
            ....
        }
        private int hash(Key key)
        {
        	return (key.hashCode() &0x7fffffff) %M;
        }
        public Value get(Key key){
    		int i = hash(key);
            for(Node x = st[i]; x! = 0; x.next)
            	if(key.equals(x.key))	return (Value)x.val;
            return null;
        }
    }

-   将key-value pairs 放在hash table上的情况（put function)


    public void put(Key key, Value val)
    {
    	int i = hash(key);
        for (Node x = st[i]; x!= null; x = x.next)
    	{
        	//如果key在chain中，将value改成现值
        	if key.equals(x.key)	x.val = val;
            //在chain st[i]的头上加上一个新的key-value pair
            else	st[i] = new Node(Key key, Val val, st[i]);
        }	
    }

### Analysis of seperate chaining

在uniform-hashing的情况下， N/M的值趋向1

Search 和insert的次数与N/M成正比

## Linear probing

Hash table中 array 的元素M大于key 的数N

-   Hash: map k to integer i between 0 and M-1
-   Insert:
    -   如果index i free,插入
    -   如果不是，找后面的位置
-   Search

    从st\[i]开始找，知道最近的一个free index如果没有就不在

### Implementation

    public class LinearProbingHashST<Key, Value>
    {
    	private int M = 30001;
        private Value[] vals = (Value[]) new Object[M];
        private Key[] keys = (Key[]) new object[M];
        private int hash(Key key)
        {//the same as before)
        public void put(Key key, Value val)
        {
        	int i;
            for(i = hash(key); keys[i] != null; i = (i+1)%M)
            	if (keys[i].equals(key))
                	break;
            keys[i] = key;
            vals[i] = val;
        }
        
         public Value get(Key key)
        {
            int i;
            for(i = hash(key); keys[i]!= null; i = (i + 1) % M)
            {
                if key.equals(keys[i])  return val[i];
            }
            return null;
        }
    }
