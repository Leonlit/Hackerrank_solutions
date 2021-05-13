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