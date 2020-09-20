
# Leetcodeͬ����ϰ������


## ��Ŀ01���ϲ�������������

> - ��ţ�21
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/merge-two-sorted-lists/

��������������ϲ�Ϊһ���µ������������ء���������ͨ��ƴ�Ӹ�����������������нڵ���ɵġ� 

**ʾ����**

```c
���룺1->2->4, 1->3->4
�����1->1->2->3->4->4
```

**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��108 ms, ������ C# �ύ�л����� 83.80% ���û�
- �ڴ����ģ�25.9 MB, ������ C# �ύ�л����� 5.85% ���û�

```c
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public ListNode MergeTwoLists(ListNode l1, ListNode l2)
    {
        ListNode pHead = new ListNode(int.MaxValue);
        ListNode temp = pHead;

        while (l1 != null && l2 != null)
        {
            if (l1.val < l2.val)
            {
                temp.next = l1;
                l1 = l1.next;
            }
            else
            {
                temp.next = l2;
                l2 = l2.next;
            }
            temp = temp.next;
        }

        if (l1 != null)
            temp.next = l1;

        if (l2 != null)
            temp.next = l2;

        return pHead.next;
    }
}
```

---
## ��Ŀ02��ɾ�����������е��ظ�Ԫ��

> - ��ţ�83
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/


����һ����������ɾ�������ظ���Ԫ�أ�ʹ��ÿ��Ԫ��ֻ����һ�Ρ�


**ʾ�� 1:**

```c
����: 1->1->2
���: 1->2
```

**ʾ�� 2:**
```c
����: 1->1->2->3->3
���: 1->2->3
```

**˼·**������˫ָ��ķ�ʽ��

`p1`��Ϊǰ���ָ��̽·��`p2`��Ϊ�����ָ���������������ظ�Ԫ�أ�`p2.next`����ȥ��`p1`�����������������ظ�Ԫ�ض���ժ������

**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��160 ms, ������ C# �ύ�л����� 5.23% ���û�
- �ڴ����ģ�25.9 MB, ������ C# �ύ�л����� 5.72% ���û�

```c
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
 
public class Solution
{
    public ListNode DeleteDuplicates(ListNode head)
    {
        if (head == null)
            return head;

        ListNode p1 = head.next;
        ListNode p2 = head;
        while (p1 != null)
        {
            if (p1.val == p2.val)
                p2.next = p1.next;
            else
                p2 = p2.next;
            p1 = p1.next;
        }
        return head;
    }
}
```

---
## ��Ŀ03����������

> - ��ţ�141
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/linked-list-cycle/

����һ�������ж��������Ƿ��л���

Ϊ�˱�ʾ���������еĻ�������ʹ������`pos` ����ʾ����β���ӵ������е�λ�ã������� 0 ��ʼ���� ���`pos`�� -1�����ڸ�������û�л���

<b>ʾ�� 1</b>��
```c
���룺head = [3,2,0,-4], pos = 1
�����true
���ͣ���������һ��������β�����ӵ��ڶ����ڵ㡣
```

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc3NldHMubGVldGNvZGUtY24uY29tL2FsaXl1bi1sYy11cGxvYWQvdXBsb2Fkcy8yMDE4LzEyLzA3L2NpcmN1bGFybGlua2VkbGlzdC5wbmc)

<b>ʾ�� 2</b>��
```c
���룺head = [1,2], pos = 0
�����true
���ͣ���������һ��������β�����ӵ���һ���ڵ㡣
```
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc3NldHMubGVldGNvZGUtY24uY29tL2FsaXl1bi1sYy11cGxvYWQvdXBsb2Fkcy8yMDE4LzEyLzA3L2NpcmN1bGFybGlua2VkbGlzdF90ZXN0Mi5wbmc)

<b>ʾ�� 3</b>��
```c
���룺head = [1], pos = -1
�����false
���ͣ�������û�л���
```
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hc3NldHMubGVldGNvZGUtY24uY29tL2FsaXl1bi1sYy11cGxvYWQvdXBsb2Fkcy8yMDE4LzEyLzA3L2NpcmN1bGFybGlua2VkbGlzdF90ZXN0My5wbmc)

<b>����</b>��

������ O(1)�������������ڴ�����������

**˼·**������˫ָ��ķ�ʽ��

ͨ������£��ж��Ƿ�������ظ���Ԫ�أ�����ʹ��`Hash`�ķ�ʽ���������ڵ���������ֳ���������Ҳ����ʹ��˫ָ��ķ�ʽ��

��һ��ָ�� `p1` ÿ���ƶ������ڵ㣬�ڶ���ָ�� `p2` ÿ���ƶ�һ���ڵ㣬�����������ڻ��Ļ�����һ��ָ��һ�����ٴ������ڶ���ָ�룬��֮���򲻴��ڻ���

���磺`head = [1,2,3,4,5]`������

```c
p1��1   3   5   2   4   1
p2��1   2   3   4   5   1
```

���磺`head = [1,2,3,4]`��ż��
```c
p1��1   3   1   3   1
p2��1   2   3   4   1
```

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 112 ms, ������ C# �ύ�л����� 98.43% ���û�
- �ڴ�����: 24.9 MB, ������ C# �ύ�л����� 5.13% ���û�

```c
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public bool HasCycle(ListNode head) {
        ListNode p1 = head;
        ListNode p2 = head;

        while (p1 != null && p1.next != null)
        {
            p1 = p1.next.next;
            p2 = p2.next;
            if (p1 == p2)
                return true;
        }
        return false;
    }
}
```

## ��Ŀ04����ת����


> - ��ţ�206
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/reverse-linked-list/

��תһ��������

<b>ʾ��</b>:
```c
����: 1->2->3->4->5->NULL
���: 5->4->3->2->1->NULL
```

<b>����</b>:

����Ե�����ݹ�ط�ת�������ܷ������ַ����������⣿

**˼·**������˫ָ��ķ�ʽ��

`p1`��Ϊǰ���ָ��̽·��`p2`��Ϊ�����ָ�������˳��������һȦ���㶨���⡣

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 116 ms, ������ C# �ύ�л����� 97.50% ���û�
- �ڴ�����: 23.3 MB, ������ C# �ύ�л����� 5.26% ���û�

```c
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */

public class Solution
{
    public ListNode ReverseList(ListNode head)
    {
        if (head == null || head.next == null)
            return head;
            
        ListNode p1 = head;
        ListNode p2 = null;
        while (p1 != null)
        {
            ListNode temp = p1.next;
            p1.next = p2;
            p2 = p1;
            p1 = temp;
        }
        return p2;
    }
}
```

---
## ��Ŀ05��ɾ�������еĽڵ�

> - ��ţ�237
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/delete-node-in-a-linked-list/

���дһ��������ʹ�����ɾ��ĳ�������и����ģ���ĩβ���ڵ㣬�㽫ֻ������Ҫ��ɾ���Ľڵ㡣

����һ������ -- head = [4,5,1,9]�������Ա�ʾΪ:

![](https://img-blog.csdnimg.cn/20190920111622847.png)


<b>ʾ�� 1</b>:
```c
����: head = [4,5,1,9], node = 5
���: [4,1,9]
����: ������������ֵΪ 5 �ĵڶ����ڵ㣬��ô�ڵ�������ĺ���֮�󣬸�����Ӧ��Ϊ 4 -> 1 -> 9.
```

<b>ʾ�� 2</b>:
```c
����: head = [4,5,1,9], node = 1
���: [4,5,9]
����: ������������ֵΪ 1 �ĵ������ڵ㣬��ô�ڵ�������ĺ���֮�󣬸�����Ӧ��Ϊ 4 -> 5 -> 9.
```

<b>˵��</b>:

- �������ٰ��������ڵ㡣
- ���������нڵ��ֵ����Ψһ�ġ�
- �����Ľڵ�Ϊ��ĩβ�ڵ㲢��һ���������е�һ����Ч�ڵ㡣
- ��Ҫ����ĺ����з����κν����



**˼·��** �����û�и��������ͷ�ڵ㣬����ֱ�Ӹ���Ҫɾ���Ľڵ㣬�����ǽ���ԭ��ɾ�������Ƕ��ڸýڵ��ǰһ���ڵ�һ����֪�������޷�ֱ��ִ��ɾ����������ˣ����ǽ�Ҫɾ���ڵ�� next �ڵ��ֵ��ֵ��Ҫɾ���Ľڵ㣬ת��ȥɾ�� next �ڵ㣬�Ӷ����Ŀ�ġ�

**�ο�����**��

- ״̬��ͨ��
- 41 / 41 ��ͨ����������
- ִ����ʱ: 120 ms, ������ C# �ύ�л����� 99.55% ���û�
- �ڴ�����: 24.4 MB, ������ C# �ύ�л����� 5.88% ���û�

```c
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */

public class Solution
{
    public void DeleteNode(ListNode node)
    {
        ListNode temp = node.next;
        while (temp != null)
        {
            node.val = temp.val;
            temp = temp.next;
            if (temp != null)
            {
                node = node.next;
            }
        }
        node.next = null;
    }
}
```



---
## ��Ŀ06���������

> - ��ţ�2
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/add-two-numbers/

�������� <b>�ǿ�</b> ������������ʾ�����Ǹ������������У����Ǹ��Ե�λ���ǰ��� <b>����</b> �ķ�ʽ�洢�ģ��������ǵ�ÿ���ڵ�ֻ�ܴ洢 <b>һλ</b> ���֡�

��������ǽ��������������������᷵��һ���µ���������ʾ���ǵĺ͡�

�����Լ���������� 0 ֮�⣬���������������� 0 ��ͷ��

<b>ʾ�� 1</b>��
```c
���룺(2 -> 4 -> 3) + (5 -> 6 -> 4)
�����7 -> 0 -> 8
ԭ��342 + 465 = 807
```

<b>ʾ�� 2</b>��
```c
���룺(3 -> 7) + (9 -> 2)
�����2 -> 0 -> 1
ԭ��73 + 29 = 102
```

**˼·**��ģ������Сѧʱ��ѧ�ļӷ����㡣��λ��ӳ���ʮ��һ��ʮλ����н�λ����Ͻ�λ���������ơ�

<b>�ο����룺</b>

- ״̬��ͨ��
- ִ����ʱ: 144 ms, ������ C# �ύ�л����� 97.98% ���û�
- �ڴ�����: 26.7 MB, ������ C# �ύ�л����� 5.07% ���û�

```c
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
public class Solution 
{
    public ListNode AddTwoNumbers(ListNode l1, ListNode l2) 
    {
        ListNode result = new ListNode(-1);
        ListNode l3 = result;
        int flag = 0;
        while (l1 != null && l2 != null)
        {
            int a = l1.val;
            int b = l2.val;
            int c = a + b + flag;
            l3.next = new ListNode(c%10);

            flag = c >= 10 ? 1 : 0;
            l1 = l1.next;
            l2 = l2.next;
            l3 = l3.next;
        }
        
        while (l1 != null)
        {
            int a = l1.val + flag;

            l3.next = new ListNode(a%10);

            flag = a >= 10 ? 1 : 0;
            l1 = l1.next;
            l3 = l3.next;
        }
        
        while (l2 != null)
        {
            int b = l2.val + flag;

            l3.next = new ListNode(b%10);
            flag = b >= 10 ? 1 : 0;
            l2 = l2.next;
            l3 = l3.next;
        }

        if (flag == 1)
        {
            l3.next = new ListNode(flag);
        }
        return result.next;        
    }
}
```

---
## ��Ŀ07��ɾ������ĵ�����N���ڵ�

> - ��ţ�19
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/

����һ������ɾ������ĵ�����`n`���ڵ㣬���ҷ��������ͷ��㡣

**ʾ��**��

```c
����һ������: 1->2->3->4->5, �� n = 2.

��ɾ���˵����ڶ����ڵ�������Ϊ 1->2->3->5.
```

**˵��**��

������`n`��֤����Ч�ġ�

**����**��

���ܳ���ʹ��һ��ɨ��ʵ����

**˼·��** ʹ������ָ�룬ǰ���ָ��`p1`����`n`���������ú����ָ��`p2`��`p1`ͬ���ߣ�`p1`�ߵ��յ㣬`p2`���ߵ�Ҫ�Ƴ��Ľ��λ�á�

**�ο����룺**
- ִ�н����ͨ��
- ִ����ʱ��104 ms, ������ C# �ύ�л����� 86.93% ���û�
- �ڴ����ģ�24.6 MB, ������ C# �ύ�л����� 100.00% ���û�

```c
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
public class Solution 
{
    public ListNode RemoveNthFromEnd(ListNode head, int n) 
    {
        ListNode p1 = head;
        ListNode p2 = head;
        
        while (n > 0)
        {
            p1 = p1.next;
            n--;
        }

        if (p1 == null) //�Ƴ�ͷ���
        {
            return head.next;
        }
            
        while (p1.next != null)
        {
            p1 = p1.next;
            p2 = p2.next;
        }
            
        p2.next = p2.next.next;
        return head;
    }
}
```


---
## ��Ŀ08���������������еĽڵ�

> - ��ţ�24
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/swap-nodes-in-pairs/

����һ���������������������ڵĽڵ㣬�����ؽ����������

**�㲻��ֻ�ǵ����ĸı�ڵ��ڲ���ֵ**��������Ҫʵ�ʵĽ��нڵ㽻����

 

**ʾ��:**

> ���� 1->2->3->4, ��Ӧ�÷��� 2->1->4->3.


**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��100 ms, ������ C# �ύ�л����� 93.18% ���û�
- �ڴ����ģ�23.4 MB, ������ C# �ύ�л����� 87.72% ���û�

```c
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
 
public class Solution
{
    public ListNode SwapPairs(ListNode head)
    {
        if (head == null || head.next == null)
            return head;

        head = Swap(head);
        
        ListNode temp = head.next;
        
        while (temp != null && temp.next != null)
        {
            temp.next = Swap(temp.next);
            if (temp.next != null)
            {
                temp = temp.next.next;
            }
        }
        return head;
    }

    public ListNode Swap(ListNode node)
    {
        if (node == null || node.next == null)
            return node;

        ListNode t = node.next;
        node.next = t.next;
        t.next = node;
        return t;
    }
}
```

---
## ��Ŀ09����ת����


> - ��ţ�61
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/rotate-list/

����һ��������ת����������ÿ���ڵ������ƶ� k ��λ�ã����� k �ǷǸ�����

**ʾ�� 1:**

```c
����: 1->2->3->4->5->NULL, k = 2
���: 4->5->1->2->3->NULL

����:
������ת 1 ��: 5->1->2->3->4->NULL
������ת 2 ��: 4->5->1->2->3->NULL
```

**ʾ�� 2:**

```c
����: 0->1->2->NULL, k = 4
���: 2->0->1->NULL

����:
������ת 1 ��: 2->0->1->NULL
������ת 2 ��: 1->2->0->NULL
������ת 3 ��: 0->1->2->NULL
������ת 4 ��: 2->0->1->NULL
```




**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��100 ms, ������ C# �ύ�л����� 98.13% ���û�
- �ڴ����ģ�25.1 MB, ������ C# �ύ�л����� 100.00% ���û�


```c
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
 
public class Solution
{
    public ListNode RotateRight(ListNode head, int k)
    {
        if (head == null || k == 0)
            return head;

        int len = GetLength(head);
        int index = len - k%len;

        if (index == len)
            return head;

        ListNode temp1 = head;
        ListNode temp2 = head;
        for (int i = 0; i < index - 1; i++)
        {
            temp1 = temp1.next;
        }
        head = temp1.next;
        temp1.next = null;

        temp1 = head;
        while (temp1.next != null)
        {
            temp1 = temp1.next;
        }
        temp1.next = temp2;
        return head;
    }

    public int GetLength(ListNode head)
    {
        ListNode temp = head;
        int i = 0;
        while (temp != null)
        {
            i++;
            temp = temp.next;
        }
        return i;
    }
} 
```



---
## ��Ŀ10���ϲ�K����������

> - ��ţ�23
> - �Ѷȣ�����
> - https://leetcode-cn.com/problems/merge-k-sorted-lists/


�ϲ� k �������������غϲ������������������������㷨�ĸ��Ӷȡ�

<b>ʾ��</b>:
```c
����:
[
  1->4->5,
  1->3->4,
  2->6
]
���: 1->1->2->3->4->4->5->6
```

<b>˼·��</b>�����ϲ��ķ�ʽ��

����ϲ�������������õ�һ���µ���������ķ�����`ListNode MergeTwoLists(ListNode l1, ListNode l2)`������ʹ�ø÷����ϲ�ǰ������������õ�һ���µ���������֮���������������������������ϲ����������ƣ����õ��ϲ�`K`�������б�����б�


**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��256 ms, ������ C# �ύ�л����� 36.69% ���û�
- �ڴ����ģ�29.3 MB, ������ C# �ύ�л����� 18.37% ���û�


```c
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
public class Solution 
{
    public ListNode MergeTwoLists(ListNode l1, ListNode l2) 
    {
        ListNode pHead = new ListNode(int.MaxValue);
        ListNode temp = pHead;

        while (l1 != null && l2 != null)
        {
            if (l1.val < l2.val)
            {
                temp.next = l1;
                l1 = l1.next;
            }
            else
            {
                temp.next = l2;
                l2 = l2.next;
            }
            temp = temp.next;
        }

        if (l1 != null)
            temp.next = l1;

        if (l2 != null)
            temp.next = l2;

        return pHead.next;
    }
    
    public ListNode MergeKLists(ListNode[] lists) {
        if (lists.Length == 0)
            return null;

        ListNode result = lists[0];
        for (int i = 1; i < lists.Length; i++)
        {
            result = MergeTwoLists(result, lists[i]);
        }
        return result;
    }
}
```








