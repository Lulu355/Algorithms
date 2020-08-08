---
title: "Algorithms"
tags: ""
---

# Union find

## Union find API

    UnionFind(int N) :initialize union-find data structure with N objects

    void union(int p, int q):链接p, q
    int find(int p): p 所在的component identifier
    boolean connected(int p, int q) 判断是否connected
    int count():component 的数量

## dynamic-connectivity client

-   从standard input 中读N个object
-   Repeat:
    -   从standard input中读pair of integers
    -   如果不相连， 连起来


    public static void main(String[],args)
    {
        int N = StdIn.readInt();
        UF uf = new UF(N)
        while(!Std.isEmpty())
        {
            int p = StdIn.readInt();
            int q = StdIn.readInt();
            if (!uf.connected(p, q))
            {
                uf.union(p, q);
                StdOut.printIn(p + " " + q);
            }
        }
    }
        

## 1.3 Bags, queues and stacks

### stacks

#### stack API

public class stackOfStrings

-   Create an empty stack

        	StackOfStrings() 

-   insert a new string onto stack

        	void push(String item)

-   remove and return the string
        	String pop()

-   is the stack empty?
        	boolean isEmpty()

-   number of strings on the stack

        	int size()

#### stack test client

要求： 如果string 为'-' 把string 从stack 上拿下， Print it
Otherwise，push string onto the stack

    public static void main(String[] args)
    {
    	StackOfStrings stack = new StackOfStrings();
        while(!StdIn.isEmpty())
        {
        	String s = StdIn.readString();
            if (s.equals("-") StdOut.print(stack.pop());
            else	stack.push(s)
        }
    }

#### Stack pop: Linked-list implementation

-   Save item to return


    String item = first.item;

-   Delete first node


    first = first.next;

-   Inner class


```
private class Node
{
	String item;
    Node next;
}

```

#### Stack push

-   Save a link to the list


    Node oldfirst = first

-   Create a new node for the beginning


    first = new Node();

-   Set the instance variables in the new node


    first.item = 'not';
    first.next = oldfirst;

#### Linked-list impletation in Java

    public class LinkedStackOfStrings
    {
    	private Node first = null;
        prive class Node
        {
        	String item;
            Node next;
        }
        public boolean isEmpty()
        { return first == null}
        
        public void push(String item)
        {
        	Node oldfirst = first;
            first = new Node();
            first.item = item;
            first.next = oldfirst;
        }
        
        public String pop()
        {
        	String item = first.item();
            first = first.next;
            return item;
        }
    }

#### Linked-list implementation performance

One item

| Structure       | Bytes |
| --------------- | ----- |
| Object Overhead | 16    |
| Extra Overhead  | 8     |
| item            | 8     |
| Next            | 8     |
| total           | 40    |

#### Array implementation

-   **s\[]** 有n个element的array
-   **push()** 将item加到第n位
-   **pop** 将Item从第n-1位移除


    public class FixedCapacityStackOfStrings
    {
    	private String[] s;
        private int N =0;
        
        public FixedCapacityStackOfStrings(int capacity)
    	
        {s = new String[capacity];}
        public boolean isEmpty()
        {return N== 0;}
        public void push(String item)
        {s[N++] = item}   # Index into array, then increment N
        public String pop()
        {return s[--N]} # decrement N, then index into array
        }
    }

### Resizing Arrays

#### Stack consideration

-   **Underflow:** It pop from an empty stack
-   **Overflow:** Use resizing array for array implemention

#### Stack: Resizing Array implementation

-   group array

    Create a new  array of twice the size, and copy items


    public ResizingArrayStackOfStrings()
    { s = new String[1]}

    public void push(String item)
    {
    	if (N == s.length) resize (2 * s.length);
        s[N++] = item;
    }
    private void resize(int capacty)
    {
    	String[] copy = new String[capacity];
        for (int i = 0; i < N; i++)
        	copy[i] = s[i];
        s = copy
    }

#### Stack: amortized cost of adding to a stack

Cost of inserting first N items:
N + (2+4+8+...+N) ~3N

#### Stack: Resizing Array implementation

push(): double size when s\[] is full

pup(): halve size when s\[] is one-quarter full

代码实现：

    public String pop(){
    	item = s[--N];
    	s[N] = null;
    	if (N > 0 && N == s.length / 4)	resize(s.length / 2);
    	return item;
    }

#### Stack resizing-array implementation: performance

| typle     | best | worst | amortized |
| --------- | ---- | ----- | --------- |
| construct | 1    | 1     | 1         |
| push      | 1    | N     | 1         |
| pop       | 1    | N     | 1         |
| size      | 1    | 1     | 1         |

#### memory usage

-   Reference to array(8 bytes)


    public class ResizingArrayStackOfStrings

-   array overhead(24 bytes)
-   array(8 \* array size)


    private String[] s;

-   int(4 bytes)


    private int N = 0;

-   padding(4 bytes)

### Queues

#### queue API

-   Create an empty queue


    QueueOfStrings()

-   insert a new string onto que


    void enqueue(String item)

-   remove and return the string


    String dequeue()

-   is the queue empty?


    boolean isEmpty()

-   number of strings on the queue


    int size()

#### Enque:linked-list implementation in Java

-   save item to return 


    String item = first.item;

-   delete first node


    first = first.next;

-   return saved item


    return item

_Note: identical to pop()_

#### dequeue

-   Save a link to the last node

```Node oldlast = last;

```

-   Create a new node for  the end

```last = new Node();
    last.item = "not"
```

-   link the new node to the next end of the list


    oldlast.next = last;

#### inner class

private class Node
{
	String item;
    Node next
}

#### linked-list impletation in Java

    public LinkedQueueOfStrings{
    	private Node first, last;
        
        private class Node{
        	String item;
            Node next;
        }
        
        public boolean isEmpty(){
        return (first == null)
        }
        public void enqueue(String item){
        	Node oldlast = last;
            last = new Node();
            last.item = String item;
            if (isEmpty() == True)	first = last;
            else{
            	oldlast.next = last;
                last.next = null
        }
        public String dequeue(){
        	String item = first.item;
            first = first.next;
            return item
        }
    }

### Generics

#### Generic Stack: linked-list implementation

    public class Stack<item> # 加上<Item>
    {
    	private Node first = null;
        prive class Node
        {
        	Item item;   # String 换为item
            Node next;
        }
        public boolean isEmpty()
        { return first == null}
        
        public void push(Item item)  # String换为item
        {
        	Node oldfirst = first;
            first = new Node();
            first.item = item;
            first.next = oldfirst;
        }
        
        public String Item pop()  # String 换为Item
        {
        	Item item = first.item(); #String 换为Item
            first = first.next;
            return item;
        }
    }

#### Generic stack: array implementation

    public class FixedCapacityStacks<Item>{		# 加<item>
    	private int N = 0;
        private Item[] s; # String[]改为Item[]
        public FixedCapacityStringOfStacks(int capacity){
        s = (Item[])new Object[capacity]; # 此处注意
        
        }
        public boolean isEmpty()
        	{return N == 0；}
        public void push(Item item){	# String改为Item
        	s[N++] = item;
        }
        public Item pop(){ 
    		s[--N] = item;
            return item;
        }
        

    ### Iterators
    - Iterable
      Has a method that returns an iterator

# iterable iterface

    pubic interface Iterable<Item>
    {
    	iterator <item> iterator();
    }

-   iterator
    has methods hasNext() & next()
    ```
    public interface Iterator<Item>
    {
    	boolean hasNext();
      Item next();
      void remove();
    }

    ```
-   Java supports client code

# Sorts

## Elementary sorts

### Rules of the game

1.Sort random real numbers in ascending order

    public class Experiment
    {
    	public static void main(String[] args)
        {
        	int N = Integer.parseInt(args[0]);
            double a = new double(N);
            for (int i = 0; i < N; i++)
            	a[i] = StdRandom.uniform();
            Insertion.sort(a)
            for (int i = 0; i< N; i++)
            	StdOut.println(a[i])
                
        }
    }

2.Sort strings from file in alphabetical order

    public class StringSorter
    {
    	public static void main(String[] args)
        {
        	String[] s = in.readAllStrings(args[0]);
            insertion.sort(s);
            for (int i = 0; i < s.length; i++)
            {
            	StdOut.println(s[i])
            }
        }
    }

3.Sort the files in a given directory by filename

    public class FileSorter
    {
    	public static void main(String[] args)
        {
        	File directory = new File(args[0]);
            File[] files = directory.listFiles();
            Insertion.sort(files);
            for (int i = 0; i < file.length; i++)
            	StdOut.println(file[i].getname())
        }
    }

#### Callbacks

In order to sort any type of data
Callback = reference to executable code

-   Client passes array of objects to sort() function
-   The sort() function call back object's compareTo() method as needed


    public class Example
    {
    	public static void sort(Comparable[] a)
        {}
        
        public static boolean less(Comparable v, Comparable w)
        {	return v.compareTo(w) < 0;}
       
        private static void exachange(Comparalbe[] a, int i, int j)
        {	Exchange the ith and jth element
        	Comparable t = a[i];
        	a[i] = a[j];
            a[j] = t;
        }
        public static void show(Comparable[] a)
        {	// for the array, on a single line
        	for (int i = 0; i < a.length; i++)
            {	StdOut.print(a[i] + " ")}
        }
        private static boolean isSorted(Comparable[] a)
        {//Test whether the array is in order	
        	for (int i = 0; i < a.length; i++)
        		if (less(a[i], a[j]))	return false;
            return ture;
        }
        public static void main(String[] args)
        {	//Read strings from standard input, sort them and print.
        	String[] a = StdIn.readAllStrings();
            sort(a);
            assert isSorted(a);
            show(a);
        }
    }

#### Comparable interface(built in to java)

    public interface Comparable<Item>
    {
    	public int compareTo(Item that);

    }

Note: `public interface Comparable<T>`
此接口强行对实现它的每个类的对象进行**整体排序**。这种排序被称为类的自然排序，类的 compareTo 方法被称为它的自然比较方法。

实现此接口的对象列表（和数组）可以通过 Collections.sort（和 Arrays.sort）进行自动排序。实现此接口的对象可以用作有序映射中的键或有序集合中的元素，无需指定比较器。

**int compareTo(T o)**
与 对象比较，小于为负整数， 等于为零， 大于为正整数

-   v.comparable(w) &lt; 0	则v &lt; w
-   v.comparable = 0	则 v = w
-   v.comparable > 0 则 v > w

Example
此接口用于特定的class

    public class Date implements Comparable<Date>
    {
        public static int compareTo(int m, int d, int y)
        {
            int year = y;
            int month = m;
            int day = d;
            if (this.year < that.year)  return -1;
            if (this.year = that.year)  return 0;
            if (this.year > that.year)  return 1;
            if (this.month < that.month)  return -1;
            if (this.month = that.month)  return 0;
            if (this.month > that.month)  return 1;
            if (this.day < that.day)  return -1;
            if (this.day = that.day)  return 0;
            if (this.day > that.day)  return 1;
            return 0;
        }
    }

### Selection Sort

不断地在剩下的array中找出最小值

    public class Selection
    {
        pubic static void sort(Comparable [] a)
        {
        	//构建未被sort的array
            N = a.length
            
            for (int i = 0; i < N; i++)
            {
                //找出剩下的array的最小值
                min = i;
                for (int j = i + 1; j < N; j++)
                {
                    if (less(a[j], a[min]))   min = j;
                }
                exch(a, i, min)
            }
        }
        
    }

#### Mathematical analysis

~N^2/2
与input无关

### Insertion sort

In iteration i, swap a/[i] with each larger entry to its left

    public class insertion
    {
        public static void sort(Comparable [] a)
        {
            int N = a.length
            // Move the pointer to right
            for (int i = 0; i < N; i++)
            {
                //Moving from right to left, exchanging a[i] with larger entry to its left
                for (int j = i; j > 0; j--)
                {
                    if less(a[j], a[j-1])   exch(a, j, j-1);
                    else    break;
                }
            }
        }
    }

#### Best and worst case

-   Worst case(Desending order) ~N^2/2
-   Average ~N^2/4
-   Best case(ascending order) ~N-1
-   Partially sorted order
    Linear
    number of exchanges 

### Shellsort

Move entries more than one position at a time by h-sorting the array 

_h-sort the array: Insertion sort with stride length h_

先间隔大的insertion sort再间隔小的insertion sort

    public class Shell
    {
    	public static void sort(Comparable[] a)
        {
        	int N = a.length;
            int h = 1;
            while(h < N/3)	h = 3 * h + 1;	//找到合适的间隔
            for (int i = h; i < N; i++)		//i的作用：从前到后依次排序
            {
            	for(int j = i; j >= h&&less(a[j], a[j-h]; j = j-h)		//j的作用：sort间隔相同的一组数
                	exch(a, j, j -h)
                h = h/3
            }
            
        }
    }
                	
                

#### analysis

The worst case: O(N^(3/2))

### Shuffle sort

1.  generate a random real number for each entry
2.  sort the array


    puclic class StdRandom
    {
    	...
        public static void shuffle(Object[] a)
        int N = a.length;
        for (int i = 0; i < N, i++)
        {
        	r = StdRandom.uniform(i + 1);
            exch(a, i, r);
        }
    }

## MergeSort

### Mergesort

**Basic plain**

1.  Devide array into two halves

    _把array\[lo, hi]分为\[lo, mid]与\[mid+1, hi]_
2.  Recursively sort each array
3.  Merge two halves

**Note: 对于a\[i++] 先赋值a\[i] 再将i 加1**

    private static void merge(Comparable[] a, lo, mid, hi)
    {
    	Comparable[] aux;
        int i = lo, j = hi;
    	for (k = lo; k <= hi; k++)
        	aux[k] = a[k]; //Copy the array a to aux
        for (k = lo; k <= hi; k++)
        {
        	if i > mid		a[k] = aux[j++];	//If left side exhaust, 直接加右侧的
            elif j > hi		a[k] = aux[i++];	//If right side exhause，直接加左侧的
            elif less(aux[i], aux[j])	aux[k] = aux[i++];
            else 	a[k] = aux[j++];
    }

**Top-down** merge sort

    public class Merge
    {
    	public static void sort(Comparable[] a)
        {
        	aux = new Comparable[a.length];		//新建一个array
        	sort(a, 0, a.length - 1);
        }
        	
    	private static void merge(Comparable[], a, lo, mid, hi)（同上）
        private static void sort(Comparable a, int lo,int hi)
        {
        	if lo >= hi		return;
            int mid = (lo + hi) / 2;
            sort(a, lo, mid);		//Sort the left part
            sort(a, mid+1, hi);		//Sort the right part
            merge(a, lo, mid, hi);		//Merge them together
        }
    }

#### analysis

The number of compares for merge
C(n) >= C(n/2) + C(n/2) + n/2
~nlgn

#### Improvement

-   对于比较小的array,采用insertion sort
-   如果a\[mid]&lt;a\[mid+1],前一半的array全部小于后一般的array，就不用merge()了
-   直接将sort好的elemnent 放到auxiliary arrray 中  
      

### bottom-up mergesort

-   pass through the array, merging subarrays of size 1
-   Repeat for subarrays of size 2,4,8...


    public class MergeBU
    {
    	public static Comparable[] aux;
        // The same as before.
        public static void sort(Comparable[] a)
        {
        	N = a.length();
            
        	for(h = 1; h < N - h; h += h * 2)
            {
            	// h为一个sort的长度
                //每次merge()是2h
            	for (lo = 0; lo < N - h; lo += 2*h)
                {
                	//注意最后的区间，当hi处于[n-h, n-1]时要分类讨论
                	merge(a, lo, lo + h -1, Math.min(lo+2*h -1, n- 1);
                }
            }
        }
    }
                	

## Quick Sort

### Quicksort

#### Basic plan

-   Shuffle the array
-   partition so that, for some j
    -   entry a\[j] is in place
    -   no larger entry to the left of j
    -   no smaller entry to the right of j
-   Sort each entry recursively

#### 步骤

1.  将i从左向右扫描，遇到比a\[0]大的就停下
2.  将j 从右向左扫描，遇到比a\[0]小的就停下
3.  当i j重合以后，与a\[0]交换

#### Code

-   [x] partition


    private static int partition(Comparable[] a, int lo, int hi)
    {
    	int i = lo;
        int j = hi + 1;
        while(true)
        {
        	while(less(a[++i], a[lo]))
            	if i == hi		break;	//Find the item on the left to swap
            while(less(a[lo], a[--j]))
            	if j == lo		break;		//Find the item on the right to swap
            if i >= j		//Check if pointers cross
            	break;		
            exch(a, i, j);		//Swap
        }
        exch(a, j, lo);
        return j;	//Return the item now known to be in place
    }

-   [x] 剩下部分


    public class Quick
    {
    	private static int partition(Comparable[] a, int lo, int hi)
        {// The same as prvious code}
        public static void(Comparable[] a)
        {
        	StdRandom.shuffle(a);
            hi = a.length - 1;
            lo = 0;
            sort(a, lo, hi);
        }
        private static void sort(Comparable[]  a, int lo, int hi)
        {
        	
            if hi <= lo		return;
            int j = partition(a, lo, hi);
            sort(a[lo, j-1]);
            sort(a[j+1, hi]);
        }
    }

#### Analysis

-   Best case	

    ~NlgN（正好均分）
-   Worst case

    ~1/2N^2（全在同一侧）
-   Average case

    ~1.39NlgN

#### Practical improvement

1.  Insertion sort small subarrays

      当array 长度足够短时用insertion sort

        private static sort(Comparable[] a, int lo, int hi)
        {
        	if hi <= lo + Cutoff - 1
           	Insertion.sort(a, lo, hi);
               return;
           else
           {
           	j = partition(a, lo, hi);
               sort(a, lo, j-1);
               sort(a, j+1, hi);
               return;
           }
        }

2.  pivot item = median

### Selection

-   Goal: Given an array of N items, find the kth smallest item
-   Example: Min(k=0), max(k=N-1), median(k=N/2)

#### 方法

j 为partition 以后return 的值，将j与k比较，判断是sort左半边还是右半边

#### Code

    public static Comparable select(Comparable[] a)
    {
    	hi = a.length - 1;
        lo = 0;
        StdRandom.shuffle(a);
        while(hi<lo)
        {
        	int j = partition(a, lo, hi);
            if (k<j)	hi = j-1;
            if(k>j)		lo = j+1;
            else	return a[j];
        }
        return a[k];
    }

#### Mathematic analysis

_Quick-select takes linear time on average_

**Number of compares:**

N+N/2+ N/4+...~2N

**Formal analysis**

2N + 2kln(N/k) + 2(N-k)ln(N/N-k)

### Duplicate

使用于一个array中有多个相同的元素的情况

#### Goal

-   依次为lo, lt, gt, hi
-   lo~lt 小于a\[lo]
-   lt~gt 等于a\[lo]
-   gt~hi 大于a\[lo]

#### 方法(a\[lo] 为v)

-   (a\[i] &lt; v) exchange a\[lt] and a\[i] increment both of lt and i
-   (a\[i] = v) increment i
-   (a\[i] > v) exchange a\[i] and a\[gt] decrement gt

#### Code

3-way quick sort

    private static void sort(Comparable[] a, int lo, int hi)
    {
    	if (hi<=lo) return;
    	int lt = lo;
        int gt = hi;
        int i = lo;
        Comparable v = a[lo];
        while(i <= gt)
        {
        	if (a[i] < v)		exch(a, i++, lt++)
            else if(a[i] = v)	i++;
            else	exch(a,i, gt--);
        }
        sort(a, lo, lt -1);
        sort(a, gt+1, hi);
    }

## Priority Queues

### API and elementary implementations

#### priority queue

-   Stack: 后进后出
-   Queue:先进后出
-   Randomized queue:random item
-   Priority:最大或最小

#### priority queue API

    public class MaxPQ<key extends Comparable <key>>

-   Create an empty priority queue
        MaxPQ()
-   Create a priority queue with given keys
        MaxPQ(Key[] a)
-   Insert a key into the priority queue
        void insert(Key v)
-   return and remove the largest key
        key delMax()
-   is priority queue empty?
        boolean isEmpty()
-   return the largest key
        key max()
-   number of entries in the priority queue
        int size()

#### priority queue client example

Find the largest M items in a stream of N items

    MinPQ<Transaction> pq = new MinPQ<Transaction>();
    while(StdIn.hasNextLine())
    {
    	String line = StdIn.readLine();
        Transaction item = new Transaction(line);
        pq.insert(item);
        if (pq.size > M)
        	pq.delMin();
    }

| implementation | time  | space |
| -------------- | ----- | ----- |
| sort           | NlogN | N     |
| elementary PQ  | MN    | M     |
| binary heap    | NlogM | M     |
| best in theory | N     | M     |

#### Priority Queue:Unordered array implementation

    public class UndorderedMaxPQ<Key extends Comparable<Key>>
    {
    	private Key[] pq;	//p[i] = ith element on pq;
        private int N;	//number of elements on pq
        public UnorderedMaxPQ(int Capacity)
        {
        	pq = (Key[]) new Comparable[capacity];
        }
        public boolean isEmpty()
        {	return N == 0;	}
        public void insert(Key x)
        { pq[N++] = x;}
        public Key delMax()
        {
        	int max = 0;
            for(int i = 1; i < N; i++)
            	if (less(max, i)) max = i;
            exch(max, N-1);
            return pq[--N];
        }
    }

Implement all operations efficiency

| implementation  | insertion | del max | max |
| --------------- | --------- | ------- | --- |
| Unordered array | 1         | N       | N   |
| Ordered array   | N         | 1       | 1   |
| Binary heap     | logN      | logN    | 1   |

### binary heaps

_Binary heaps: Array representation of a heap-ordered complete binary tree_

-   Heap-ordered binary tree
    -   Keys in nodes
    -   Parent's key no smaller than children's keys

-   Array representation
    -   Indices start at 1
    -   Take nodes in level order
    -   No explicit links needed

-   Can use array indices to move through tree
    -   Parent of node at k is at k/2
    -   Children of node at k are at 2k and 2k+1

#### Promotion in a heap

_Child's key becomes larger than its parent's key_

方法

-   exchange key in child with key in parent
-   Repeat until heap order restored


    private void swim(int k)
    {
    	while(k > 1 && less(k/2, k))
        {
        	exch(k/2, k);
            k = k/2;
        }
    }

#### Insertion in the heap

Add node at end and swim it up
Cost:最多1+lgN

    public void insert(Key x)
    {
    	pq[++N] = x;
        swim(N);
    }

#### Demotion in a heap

_Parent's key becomes smaller than one of child's key_

-   exchange key in parent with key in larger child
-   Repeat until heap order restored


    private void sink(int k)
    {
    	while (2*k <= N)
        {
        	int j = 2*k;
            if (j< N && less(j, j+1))	j++;
            if (less(j, k))	 break;
            exch(j, k);
            k = j;
        }
    }

#### Delete the maximum in a heap

Exchange root with node at end, then sink it down

    public Key delMax()
    {
    	Key max = pq[1];
        exch(1, N--);
        sink(1);
        pq[N+1] = null;
        return max;
    }

### heapsort

#### Basic plan

-   Create max-heap with all N keys
-   Repeatedly remove the maximum key

#### Heap Construction

-   Build max heap using bottom-up method
        for(k = N/2; k >= 1; k--)
        	sort(a, k, N);
-   Remove the maximum, one at a time
        while(N > 1)
        {
        	exch(a, 1, N--);
        	sink(a, 1, N);
        }

#### Java implementation

    public class Heap
    {
    	public static void sort(Comparable[] a)
        {
        	int N = a.length;
            for(int k = N/2; k >= 1; k--)
            	sink(a, k, N);
            while(N >1)
            {
            	exch(a, 1, N--);
                sink(a, 1, --N);
            }
        }
    }
    private static void sink(Comparable [] a, int k, int N)
    {/*The same as before*/}

    }

#### Mathematical analysis

-   Heap construction uses &lt;= 2N compares and exchanges
-   Heapsort uses &lt;= 2NlgN compares and exchanges.
-   In-place sorting algorithm with NlogN  worst-case

### event-driven simulation
