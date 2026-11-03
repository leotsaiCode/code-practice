# Solution

C#

```csharp
    // Brute Force Time: O(N), Space: O(1) 2 Pass
    public static SinglyLinkedListNode removeKthNodeFromEnd(SinglyLinkedListNode head, int k)
    {
        var node = head;
        var lens = 0;

        while(node != null){
            lens++;
            node= node.next;
        }

        var index = lens -1-k;

        if(index<0)
            return  head;
        if(index == 0)
            return head.next;

        var node2 = head;

        for(int i = 0;i<index - 1;i++){
            node2= node2.next;
        }

            node2.next = node2.next.next;
        return head;
    }

    // save to list Time: O(N), Space: O(N) 1 pass
    public static SinglyLinkedListNode removeKthNodeFromEnd(SinglyLinkedListNode head, int k)
    {
        var node = head;
        var list = new List<SinglyLinkedListNode>();

        while(node != null){
            list.Add(node);
            node= node.next;
        }

        var toRemoveItemIndex = lens -1-k;

        if(toRemoveItemIndex<0)
            return  head;
        if(toRemoveItemIndex == 0)
            return head.next;

        var prevNode = list[toRemoveItemIndex - 1];
            prevNode.next = prevNode.next.next;

        return head;
    }

    // two pointers fast over slow k+2 steps to remove k+1 node
    // k is reverse "index"
    public static SinglyLinkedListNode removeKthNodeFromEnd(SinglyLinkedListNode head, int k)
    {
        var fast = head;
        var slow = head;
        int lens = 0;

        while(fast != null){
            fast= fast.next;

            if(lens >= k+2){
                slow= slow.next;
            }

            lens+=1;
        }

        if (k >= lens)
            return head; // delete invalid

        if (k == lens - 1)
            return head.next;  // delete Head

        slow.next = slow.next.next;
        return head;
    }
```

```

```
