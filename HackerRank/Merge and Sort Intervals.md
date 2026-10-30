# Solutions

```csharp
public static List<List<int>> mergeHighDefinitionIntervals(List<List<int>> intervals)
{
var result = new List<List<int>>();
if(intervals.Count ==0)
return result;

        intervals.Sort((a, b) => a[0].CompareTo(b[0]));

        result.Add(intervals[0]);

        for(int i = 1; i< intervals.Count;i++)
        {
            if(intervals[i][0]<= result.Last()[1])
            {
                if(intervals[i][1] >result.Last()[1])
                    result.Last()[1] = intervals[i][1];
            }
            else{
                result.Add(intervals[i]);
            }

        }

        return result;
    }
}
```

ChatGPT's Answer

```csharp
public static List<List<int>> mergeHighDefinitionIntervals(List<List<int>> intervals)
{
    var result = new List<List<int>>();

    if (intervals.Count == 0)
        return result;

    intervals.Sort((a, b) => a[0].CompareTo(b[0]));

    result.Add(new List<int>(intervals[0]));

    for (int i = 1; i < intervals.Count; i++)
    {
        var last = result[result.Count - 1];
        var current = intervals[i];

        if (current[0] <= last[1])
        {
            last[1] = Math.Max(last[1], current[1]);
        }
        else
        {
            result.Add(new List<int>(current));
        }
    }

    return result;
}
```
