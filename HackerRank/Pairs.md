> brute force: check every pair
> Time O(n^2) Space O(1)

```csharp
public static int pairs(int k, List<int> arr)
{
    var pairs = 0;
    for(var i = 0; i<arr.Count;i++)
    {
        for(var j = i+1;j<arr.Count;j++)
        {
            if(Math.Abs(arr[i] - arr[j]) == k)
                pairs+=1;
        }
    }

    return pairs;
}
```

> i, j version gets timeout error on HackerRank, so use HashSet to look up (num + k) instead
> Time O(n) Space O(n)

```csharp
public static int pairs(int k, List<int> arr)
{
    var numbers = new HashSet<int>(arr);
    var pairs = 0;

    foreach (var num in arr)
    {
        if(numbers.Contains(num+k))
            pairs+=1;
    }

    return pairs;
}
```
