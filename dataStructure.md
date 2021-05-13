# Solutions for Hackerrank Data Structure Challenges.

## Dynamic Array

``` java
public static List<Integer> dynamicArray(int n, List<List<Integer>> queries) {
    ArrayList<ArrayList<Integer>> arr = new ArrayList<ArrayList<Integer>>(n);
    ArrayList<Integer> answer = new ArrayList<Integer>();
    int l_A = 0;
    for (int x=0;x<queries.size();x++) {
        List<Integer> curr = queries.get(x);
        int idx = ((curr.get(1) ^ l_A) % n);
        try {
            if (curr.get(0) == 1) {
                arr.get(idx).add(curr.get(2));
            }else {
                l_A = arr.get(idx).get(curr.get(2) % arr.get(idx).size());
                answer.add(l_A);
            }
        }catch (IndexOutOfBoundsException ex) {
            x--;
            //if the index is out of bounds, means that we need to increase the size of our array list.
            while (arr.size() < idx + 1) {
                arr.add(new ArrayList<Integer>());
            }
        } 
    }
    return answer;
}
```

## Array Left Rotation

``` java
public static List<Integer> rotateLeft(int d, List<Integer> arr) {
    int size = arr.size();
    Integer newArr[] = new Integer[size];
    for (int x=0;x<size;x++) {
        newArr[(size - (d - x)) % size] = arr.get(x);
    }
    return Arrays.asList(newArr);
}
```


## Sparse Array

```java
public static List<Integer> matchingStrings(List<String> strings, List<String> queries) {
    int arr[] = new int[queries.size()];
    int s_size = strings.size();
    int q_size = queries.size();
    for (int x=0;x<s_size;x++) {
        String curr = strings.get(x);
        for (int y=0;y<q_size;y++) {
            if (curr.compareTo(queries.get(y)) == 0) {
                arr[y] += 1;
            }
        }
    }
    for (int x = 0;x< arr.length;x++) {
        System.out.println(arr);
    }
    return Arrays.stream(arr).boxed().collect(Collectors.toList());
}
```

## Array Manipulation

### Brute force solution
``` java
public static long arrayManipulation(int n, List<List<Integer>> queries) {
// Write your code here
    long arr[] = new long[n];
    long max = Long.MIN_VALUE;
    for (int x=0;x<queries.size();x++) {
        List<Integer> curr = queries.get(x);
        int start = curr.get(0);
        int end = curr.get(1);
        long value = curr.get(2);
        for (int y = start - 1;y < end;y++) {
            arr[y] += value;
            if(max < arr[y]) max = arr[y];
        }
    }
    return max;
}
```

### Prefix sum solution
``` java
public static long arrayManipulation(int n, List<List<Integer>> queries) {
// Write your code here
    long arr[] = new long[n + 1];
    for (int x=0;x<queries.size();x++) {
        List<Integer> curr = queries.get(x);
        int start = curr.get(0);
        int end = curr.get(1);
        int value = curr.get(2);
        arr[start - 1] += value;
        arr[end] -= value;
    }
    System.out.println(Arrays.toString(arr));
    long max = 0;
    long sum = 0;
    for (int x=0;x<arr.length;x++ ) {
        sum += arr[x];
        max = Math.max(sum, max);
    }
    return max;
}
```