#

C#

```csharp
    // Hidden test will fail
    public static bool areBracketsProperlyMatched(string code_snippet)
    {
        var nestedList = new List<string>();
        foreach(var ch in code_snippet.Split()){
            if(ch is "{" or "}" or"[" or "]" or "(" or ")" )
            {
                if(ch is "{" or"["  or "("){
                    nestedList.Add(ch);
                }
                else{
                    switch(ch){
                        case "}":
                            if(nestedList.LastOrDefault() is "{")
                                nestedList.RemoveAt(nestedList.Count - 1);
                            else
                                return false;
                        break;
                        case "]":
                            if(nestedList.LastOrDefault() is "[")
                                nestedList.RemoveAt(nestedList.Count - 1);
                            else
                                return false;
                        break;
                        case ")":
                            if(nestedList.LastOrDefault() is "(")
                                nestedList.RemoveAt(nestedList.Count - 1);
                            else
                                return false;
                        break;
                    }

                }
            }
        }
        if(nestedList.Count > 0)
            return false;

        return true;
    }


    // first version with stack
    public static bool areBracketsProperlyMatched(string code_snippet)
    {
        var stack = new Stack<char>();
        foreach(var ch in code_snippet){
            if(ch is '{' or '}' or'[' or ']' or '(' or ')' )
            {
                if(ch is '{' or'['  or '('){
                    stack.Push(ch);
                }
                else{
                    switch(ch){
                        case '}':
                            if(stack.TryPeek(out var topL) && topL is '{')
                                stack.Pop();
                            else
                                return false;
                        break;
                        case ']':
                            if(stack.TryPeek(out var topM)&& topM is '[')
                                stack.Pop();
                            else
                                return false;
                        break;
                        case ')':
                            if(stack.TryPeek(out var topS)&& topS is '(')
                                stack.Pop();
                            else
                                return false;
                        break;
                    }

                }
            }
        }
        if(stack.Count > 0)
            return false;

        return true;

    }

    // second version
    public static bool areBracketsProperlyMatched(string code_snippet)
    {
        var stack = new Stack<char>();

        foreach (char ch in code_snippet)
        {
            if (ch is '(' or '[' or '{')
            {
                stack.Push(ch);
                continue;
            }

            if (ch is not (')' or ']' or '}'))
                continue;

            if (!stack.TryPop(out char open))
                return false;

            if ((open == '(' && ch != ')') ||
                (open == '[' && ch != ']') ||
                (open == '{' && ch != '}'))
                return false;
        }

        return stack.Count == 0;
    }
```
