---
title: appendix-b
date: 2017-05-02 01:05:54
tags:
- Java
category:
- 编程
---

# Exam Appendix -- Java Quick Reference

Accessible methods from the Java library that may be included on the exam

```java
class java.lang.Object {
	boolean equals(Object other);
	String toString();
}
```

```java
class java.lang.Integer {
	Integer(int value);
	int intValue();
	/** Minimum value represented by an `int` or `Integer`. */
	static int MIN_VALUE;
	/** Maximum value represented by an `int` or `Integer`. */
	static int MAX_VALUE;
}
```

```java
class java.lang.Double {
	Double(double value);
	double doubleValue();
}
```

```java
class java.lang.String implements java.lang.Comparable<String> {
	int length();
	/**	@return the substring beginning at `from` and ending at `to-1`.	 Note: the substring has length of `to - from`.	*/
	String substring(int from, int to);
	/** @return `substring(from, length())`. */
	String substring(int from);
	/** @return the index of the first occurrence of `str`; -1 if not found. */
	int indexOf(String str);
	/** @return value < 0 if `this` less than `other`; 0 if equals to `other`; > 0 if greater than `other`. */
	int compareTo(String other);
}
```

```java
class java.lang.Math {
	static int abs(int x);
	static double abs(double x);
	static double pow(double base, double exponent);
	static double sqrt(double x);
	static double random();
}
```

```java
interface java.util.List<E> {
	int size();
	/** Appends obj to end of list.	@return `true` Note: only if operation allowed, such as always true for `ArrayList`. */
	boolean add(E obj);
	/** Inserts `obj` at position `index`, for 0 ≤ `index` ≤ `size()`. */
	void add(int index, E obj)
	E get(int index);
	/** Replaces the element at position `index` with `obj`.
	@return the element formerly at the specified position. */
	E set(int index, E obj);
	/** Removes element from position `index`, moving elements at position `index + 1` and higher to the left by 1 (subtracts 1 from their indices) and adjusts size. @return the element formerly at the specified position. */
	E remove(int index);
}
```

```java
class java.util.ArrayList<E> implements java.util.List<E> { }
```