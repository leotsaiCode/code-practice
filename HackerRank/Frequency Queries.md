> Dictionary stores the count of each number; query 3 uses ContainsValue to check if any number appears query[1] times
> ContainsValue scans the whole Dictionary, so it gets a timeout on HackerRank
> Time O(n^2) Space O(n)

```csharp
    static List<int> freqQuery(List<List<int>> queries) {
        var result = new List<int>();
        var numCountDict = new Dictionary<int,int>();
        
        foreach(var query in queries)
        {
            switch(query[0])
            {
                case 1:
                    if(!numCountDict.TryAdd(query[1],1))
                        numCountDict[query[1]] +=1;
                    break;    
                case 2:
                    if(numCountDict.TryGetValue(query[1], out var count) && count > 0)
                        numCountDict[query[1]] -=1;
                    break;
                case 3:
                    if(numCountDict.ContainsValue(query[1]))
                        result.Add(1);
                    else
                        result.Add(0);
                    break;
            }
        }
        
        return result;
    }
```

> Add a frequencyCountDict that maps "count -> how many numbers have this count"
> On query 1 and 2, update the tally of both the old count and the new count; query 3 just looks up frequencyCountDict in O(1)
> A number whose count drops to 0 is removed from numCountDict and is not counted in frequencyCountDict
> Time O(n) Space O(n)

```csharp
   static List<int> freqQuery(List<List<int>> queries) {
        var result = new List<int>();
        
        var numCountDict = new Dictionary<int, int>();
        var frequencyCountDict = new Dictionary<int, int>();

        foreach (var query in queries)
        {
            var operation = query[0];
            var number = query[1];

            switch (operation)
            {
                case 1:
                {
                    numCountDict.TryGetValue(number, out var oldCount);
                    var newCount = oldCount + 1;
                    if (oldCount > 0)
                        frequencyCountDict[oldCount]--;
                        
                    frequencyCountDict.TryAdd(newCount, 0);
                    frequencyCountDict[newCount]++;

                    numCountDict[number] = newCount;
                    break;
                }

                case 2:
                {
                    if (!numCountDict.TryGetValue(number, out var oldCount)
                        || oldCount == 0)
                        break;

                    var newCount = oldCount - 1;

                    frequencyCountDict[oldCount]--;

                    if (newCount > 0)
                    {
                        frequencyCountDict.TryAdd(newCount, 0);
                        frequencyCountDict[newCount]++;
                        numCountDict[number] = newCount;
                    }
                    else
                    {
                        numCountDict.Remove(number);
                    }

                    break;
                }

                case 3:
                {
                    if (frequencyCountDict.TryGetValue(number, out var count)
                        && count > 0)
                        result.Add(1);
                    else
                        result.Add(0);

                    break;
                }
            }
        }

        return result;
    }
```
