# Solutions

```csharp
public static int countResponseTimeRegressions(List<int> responseTimes)
{
    var result = 0;

    for (var i = 0; i < responseTimes.Count; i++)
    {
        if (i == 0)
            continue;
        long preSum = 0;

        for (var j = 0; j < i; j++)
        {
            preSum += responseTimes[j];
        }

        if (responseTimes[i] > (preSum / i))
            result += 1;

    }

    return result;
}

```

```go
func countResponseTimeRegressions(responseTimes []int32) int32 {
    // Write your code here
    var count int32 = 0;
    for i := 1; i< len(responseTimes); i++{

        var preSum int64

        for j:=0; j < i; j++{
            preSum+= int64(responseTimes[j])

        }
        if int64(responseTimes[i])>(preSum/int64(i)){
            count++
        }
    }

    return count;
}
```
