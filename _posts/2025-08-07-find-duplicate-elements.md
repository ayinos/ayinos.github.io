---
title: Find duplicate elements in a list
date: 2025-07-19 10:43:20 +/-TTTT
categories: [Java, Stream API]
tags: [java8,stream,list,set,filter]     # TAG names should always be lowercase
---

## Solution 1: Use a set
```java

List<String> colors = List.of("Red", "Blue", "Green", "Blue", "Purple", "Green");
HashSet<String> uniqueColors = new HashSet();
HashSet<String> duplicateColors = 
  colors.stream()
  .filter(color -> !uniqueColors.add(color))//add() returns false if value already exists.
  .collect(Collectors.toSet()); //collect into a set.
```

## Solution 2: Use a hashmap to store the frequency
```java
List<String> colors = List.of("Red", "Blue", "Green", "Blue", "Purple", "Green");
HashSet<String> duplicateColors = 
  colors.stream()
  //Step 1 : Create a map with keys as the values in the stream & the frequency as the value
  .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
  //Step 2 : Select the colors with frequency > 1
  .entrySet() //Convert the map to a stream
  .filter(entry -> entry.getValue() > 1)//returns entry
  .map(entry -> entry.getKey())//returns key i.e. color
  .collect(Collectors.toSet()); //collect into a set.

```

## Solution 3: Use Collections.frequency() to find the frequency.
#### Function : Collections.frequency()
#### Parameters:
1. The collection in which to search for the element (colors).
2. The object whose frequency is to be determined (color).
#### Return value:
The method returns an int representing the total count of elements in the collection that are equal to the specified object.

```java
List<String> colors = List.of("Red", "Blue", "Green", "Blue", "Purple", "Green");
HashSet<String> duplicateColors =
  colors.stream()
  .filter(color -> Collections.frequency(colors, color) > 1)//returns entry
  .collect(Collectors.toSet()); //collect into a set.

```
