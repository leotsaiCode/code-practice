> Dictionary stores the count of each word in note; while iterating magazine, decrement on a match and remove at 0
> On every match, check Count == 0 and break early
> Time O(n + m) Space O(n)

```csharp
public static void checkMagazine(List<string> magazine, List<string> note)
{
    var noteWordCountDict = new Dictionary<string, int>();
    var result = false;
    if(note.Count > magazine.Count)
    {
        Console.WriteLine("No");
        return;
    }

    foreach(var word in note)
    {
         if(!noteWordCountDict.TryAdd(word, 1))
             noteWordCountDict[word] +=1;
    }

    foreach(var word in magazine)
    {
        if(noteWordCountDict.TryGetValue(word, out var count))
        {
            if(count == 1)
                noteWordCountDict.Remove(word);
            else
                noteWordCountDict[word] -=1;

            if(noteWordCountDict.Count == 0)
            {
                result = true;
                break;
            }
        }
    }

    Console.WriteLine(result is true ? "Yes":"No");
}
```

> Remove a word from the Dictionary when its count hits 0; Count == 0 means every word in note has been matched
> No result variable; the Count check moves outside the loop, which keeps the logic simpler
> Time O(n + m) Space O(n)

```csharp
public static void checkMagazine(List<string> magazine, List<string> note)
{
    var noteWordCountDict = new Dictionary<string, int>();

    foreach(var word in note)
    {
        noteWordCountDict[word] = noteWordCountDict.GetValueOrDefault(word) + 1;
    }

    foreach(var word in magazine)
    {
        if(!noteWordCountDict.TryGetValue(word, out var count))
            continue;

        if(count == 1)
            noteWordCountDict.Remove(word);
        else
            noteWordCountDict[word] = count - 1;
    }

    Console.WriteLine(noteWordCountDict.Count == 0 ? "Yes" : "No");
}
```
