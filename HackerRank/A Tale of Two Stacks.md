> use two stacks to implement queue, stack1 for enqueue, stack2 for dequeue / peek
> only move all elements from stack1 to stack2 when stack2 is empty, the order is reversed so top of stack2 is the front of queue
> Time amortized O(1) per query (each element is moved at most once) Space O(n)

```csharp
static void Main(String[] args) {
    var stack1 = new Stack<int>();
    var stack2 = new Stack<int>();

    var queryCount = int.Parse(Console.ReadLine()!);

    for(var i = 0;i < queryCount; i++ )
    {
        var parts = Console.ReadLine()!.Split(' ');
        var operation = int.Parse(parts[0]);

        if(operation is 1)
        {
            stack1.Push(int.Parse(parts[1]));
        }
        else
        {
            if(stack2.Count == 0)
            {
                while(stack1.Count > 0)
                {
                    if(stack1.TryPop(out var element))
                        stack2.Push(element);
                }
            }
            if(operation == 2)
                stack2.TryPop(out var element);

            if(operation == 3)
            {
                stack2.TryPeek(out var element);
                Console.WriteLine(element);
            }
        }

    }
}
```
