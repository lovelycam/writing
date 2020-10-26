## findNeedles

```java
public static void findNeedles(String haystack, String[] needles)
```

Searches a `haystack` string for values specified in the `needles` string array.

#### Parameters

Parameter | Explanation
------------ | -------------
`haystack` | The string to be searched.
`needles` | The string array values to search for (maximum of 5).

#### Output
The `needles` strings and the number of times each string was found.

#### Usage
```java
String haystack = "layla lisa";
String[] needles = {"layla", "lisa", "chris", "caleb"};
findNeedles(haystack, needles);
```

The following is printed in the console:

```java
layla: 1
lisa: 1
chris: 0
caleb: 0
```

#### Implementation Details

The `findNeedles` method accepts two arguments: `haystack` (a string), and `needles` (a string array). Each string in the `needles` array is compared against delimited words in the `haystack` string. Comparisons are case-sensitive.

Words in the `haystack` string can be delimited by any of the following:

- spaces
- double quotation marks
- single quotation marks
- tab characters
- new lines
- word boundaries
- form feeds
- carriage returns

The `findNeedles` method delimits `haystack` words by calling Java’s `split` method and passing a delimiting regular expression:

```java
String[] words = haystack.split("[ \"\'\t\n\b\f\r]", 0);
```

The `split` method stores an array of strings in `words`. The `words` strings are then compared to strings in the `needles` string array. A `countArray` integer array keeps track of the number of matched instances, as demonstrated below:

```java
int[] countArray = new int[needles.length];
for (int i = 0; i < needles.length; i++) {
	for (int j = 0; j < words.length; j++) {
		if (words[j].compareTo(needles[i]) == 0) {
			countArray[i]++;
		}
	}
}
```
