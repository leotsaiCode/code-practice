# Solutions

C#

> have done LeetCode 3 before, so I immediately thought of using a sliding window.

```csharp

public static int maxDistinctSubstringLengthInSessions(string sessionString)
{
    var charLastShowIndexDict  = new Dictionary<char,int>();
    var maxLens = 0;
    var eachSessionString = sessionString.Split("*");


    foreach(var str in eachSessionString)
    {
        var leftIndex = 0;
        charLastShowIndexDict.Clear();

        for(var rightIndex= 0;rightIndex<str.Length;rightIndex++)
        {
            var rightChar = str[rightIndex];
            if(charLastShowIndexDict.TryGetValue(rightChar ,out int dictIndex) &&
                dictIndex >= leftIndex)
            {
                leftIndex = dictIndex +1;
            }

            var curLens = rightIndex - leftIndex +1;

            maxLens = maxLens > curLens ? maxLens : curLens;

            charLastShowIndexDict[rightChar] = rightIndex;
        }
    }

    return maxLens;
}
```
