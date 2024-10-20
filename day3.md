## 203.移除链表元素
- **题目：给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点 。**
    ```csharp
    public ListNode RemoveElements(ListNode head, int val) 
    {
        ListNode he=new ListNode(0,head);
        ListNode l=he;
        while(l.next != null)
        {
            if(l.next.val==val)
            {
                l.next=l.next.next;
            }else{l=l.next;}
        }
        return he.next;
    }
    ```
## 707.设计链表  
- **题目：实现一个 MyLinkedList 类：**
    
    **在链表类中实现这些功能：**
    
    **get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。**
    
    **addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。**
    
    **addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。**
    
    **addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。**
    
    **deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。**
    ```csharp
    public class listnode
    {
        public int val;
        public listnode next=null;
        public listnode(int val, listnode next)
        {
             this.val = val;
             this.next = next;
        }
    }
    public class MyLinkedList
    {
        //虚拟头节点
        public listnode dummyhead = new listnode(0, null);
        //链表长度
        public int count = 0;
        public MyLinkedList()
        {}
        public int Get(int index)
        {
            int i = -1;
            listnode nownode = dummyhead;
            while (nownode.next != null)
            {
                nownode = nownode.next;
                i++;
                if (i == index)
                {
                    return nownode.val;
                }
            }
            return -1;
        }
        public void AddAtHead(int val)
        {
            listnode newnode = new listnode(val, dummyhead.next);
            dummyhead.next = newnode;
            count++;
        }
        public void AddAtTail(int val)
        {
            AddAtIndex(count,val);
        }
        public void AddAtIndex(int index, int val)
        {
             listnode nownode = dummyhead;
             if (index <= 0) { AddAtHead(val); }
            else
            {
                int i = -1;
                while (nownode.next != null)
                {
                    i++;
                    if (index == i)
                    {
                        listnode newnode = new listnode(val, nownode.next);
                        nownode.next = newnode;
                        count++;
                    }
                    nownode = nownode.next;
                }
                if (index == count)
                {
                    listnode newnode = new listnode(val, null);
                    nownode.next = newnode;
                    count++;
                }
            }
        }
         public void DeleteAtIndex(int index)
         {
             if (index > -1 && index < count)
             {
                 listnode nowlist=dummyhead;
                 int i = -1;
                 while (nowlist.next!=null) 
                 {
                     i++;
                     if (index == i)
                     {
                         nowlist.next=nowlist.next.next;
                         count--;
                         return;
                     }
                     nowlist=nowlist.next;     
                 }
             }
         }
     }
    ```
    
## 206.反转链表 
- **题意：反转一个单链表。**
    
    **示例: 输入: 1->2->3->4->5->NULL 输出: 5->4->3->2->1->NULL**
    1. ### 双指针法
        - #### 创建两个指针，一个指向虚拟头结点节点，一个指向头结点节点，通过不断向后移动，交换节点，实现链表反转。
        ```csharp
         public ListNode ReverseList(ListNode head)
          {
              ListNode newhead = head;
              ListNode newtail = null;
              if (head != null) {
                  while (newhead.next != null)
                  {
                      ListNode temp = newhead.next;
                      newhead.next = newtail;
                      newtail = newhead;
                      newhead = temp;
                  }
                  newhead.next=newtail;
              }
              
              return newhead;
          }
        ```