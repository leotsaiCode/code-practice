> Dictionary 存 note 每個字的出現次數，跑 magazine 時對到就 -1，歸 0 就移除
> 每次對到都要檢查 Count == 0，提早 break
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

> 歸 0 就從 Dictionary 刪除，Count == 0 即代表 note 的字都湊齊
> 不用 result 變數，Count 檢查移到迴圈外，邏輯更簡單
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
