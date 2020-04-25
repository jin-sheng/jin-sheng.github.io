# 二分查找
```java
public static int binarySearch(int[] array, int target)
{
    if (array == null)
    {
        return -1;
    }
    int left = 0, right = array.length - 1;
    while (left <= right)
    {
        int middle = (left + right) / 2;
        if (target == array[middle])
        {
            return middle;
        }
        if (target > array[middle])
        {
            left = middle + 1;
        }
        else
        {
            right = middle - 1;
        }
    }
    return -1;
}
```
