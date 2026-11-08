```csharp
class Solution
{
    static void Main(string[] args)
    {
        var input = Console.In.ReadToEnd()
            .Split(
                new[] { ' ', '\n', '\r', '\t' },
                StringSplitOptions.RemoveEmptyEntries
            );

        int count = int.Parse(input[0]);
        Node root = null;

        for (int i = 0; i < count; i++)
        {
            int value = int.Parse(input[i + 1]);
            root = Insert(root, value);
        }

        LevelOrder(root);
    }

    static Node Insert(Node root, int value)
    {
        if (root == null)
            return new Node(value);

        var current = root;

        while (true)
        {
            if (value < current.Value)
            {
                if (current.Left == null)
                {
                    current.Left = new Node(value);
                    break;
                }

                current = current.Left;
            }
            else if (value > current.Value)
            {
                if (current.Right == null)
                {
                    current.Right = new Node(value);
                    break;
                }

                current = current.Right;
            }
            else
            {
                break;
            }
        }

        return root;
    }

    static void LevelOrder(Node root)
    {
        if (root == null)
            return;

        var queue = new Queue<Node>();
        queue.Enqueue(root);

        while (queue.Count > 0)
        {
            var currNode = queue.Dequeue();

            if (currNode.Left != null)
                queue.Enqueue(currNode.Left);

            if (currNode.Right != null)
                queue.Enqueue(currNode.Right);

            Console.Write(currNode.Value);

            if (queue.Count > 0)
                Console.Write(" ");
        }

        Console.WriteLine();
    }

    class Node
    {
        public Node Left { get; set; }
        public Node Right { get; set; }
        public int Value { get; set; }

        public Node(int value)
        {
            Value = value;
        }
    }
}
```
