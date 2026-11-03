# Solution

C#

```csharp
    // Brute Force  Time Complex O(n) Capacity Complex O(n)
    public static bool isAlphabeticPalindrome(string code)
    {
        var lowerLetterString = Regex.Replace(code, "[^a-zA-Z]", "").ToLower();
        if(lowerLetterString.Length == 1)
            return true;
        var stacks = new List<List<char>>();
        var tempStack = new List<char>();
        var isOdd = lowerLetterString.Length%2 == 1;
        var halfIndex = lowerLetterString.Length/2;
        for(int i = 0;i<halfIndex;i++){
            tempStack.Add(lowerLetterString[i]);
        }
        stacks.Add(new List<char>(tempStack));
        tempStack.Clear();
        for(int i = lowerLetterString.Length -1 ; i >= (isOdd? halfIndex+1 :halfIndex);i--){
            tempStack.Add(lowerLetterString[i]);
        }
        stacks.Add(new List<char>(tempStack));
        return stacks[0].SequenceEqual(stacks[1]);
    }


    // Stack  Time Complex O(n) Capacity Complex O(n)
    public static bool isAlphabeticPalindrome(string code)
    {
        var lowerLetterString = Regex.Replace(code, "[^a-zA-Z]", "").ToLower();

        if(lowerLetterString.Length == 1)
            return true;

        var tempStack = new List<char>();

        var isOdd = lowerLetterString.Length%2 == 1;
        var halfIndex = lowerLetterString.Length/2;

        for(int i = 0; i< lowerLetterString.Length;i++){
            if(i >= halfIndex){
                if(i == halfIndex && isOdd)
                    continue;

                if(tempStack.Last() == lowerLetterString[i])
                    tempStack.RemoveAt(tempStack.Count - 1);
            }
            else{
                tempStack.Add(lowerLetterString[i]);
            }
        }


        return tempStack.Count == 0;
    }

    // 0 len string also is Palindrome Stack  Time Complex O(n) Capacity Complex O(n)
    public static bool isAlphabeticPalindrome(string code)
    {
        var lowerLetterString = Regex.Replace(code, "[^a-zA-Z]", "").ToLower();

        var lens = lowerLetterString.Length;

        var result = true;
        var halfIndex = lens/2;

        for(int i = 0; i< halfIndex;i++){
            if(lowerLetterString[i] == lowerLetterString[lens-1-i])
            {
                continue;
            }
            else{
                result = false;
                break;
            }
        }

        return result;
    }
```

ChatGPT's Answer

```csharp
public static bool isAlphabeticPalindrome(string code)
{
    int left = 0;
    int right = code.Length - 1;

    while (left < right)
    {
        if (!IsEnglishLetter(code[left]))
        {
            left++;
            continue;
        }

        if (!IsEnglishLetter(code[right]))
        {
            right--;
            continue;
        }

        if (char.ToLowerInvariant(code[left]) !=
            char.ToLowerInvariant(code[right]))
        {
            return false;
        }

        left++;
        right--;
    }

    return true;

    bool IsEnglishLetter(char c)
    {
        return (c >= 'a' && c <= 'z') ||
            (c >= 'A' && c <= 'Z');
    }
}
```
