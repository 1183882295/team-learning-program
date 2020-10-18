# Leetcodeͬ����ϰ���ģ�

## ��Ŀ01����Сջ

> - ��ţ�155
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/min-stack/

���һ��֧�� push��pop��top �����������ڳ���ʱ���ڼ�������СԪ�ص�ջ��

- push(x) -- ��Ԫ�� x ����ջ�С�
- pop() -- ɾ��ջ����Ԫ�ء�
- top() -- ��ȡջ��Ԫ�ء�
- getMin() -- ����ջ�е���СԪ�ء�

<b>ʾ��</b>:

```c
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> ���� -3.
minStack.pop();
minStack.top();      --> ���� 0.
minStack.getMin();   --> ���� -2.
```

**˼·**�����ø���ջ�ķ�ʽ��

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 192 ms, ������ C# �ύ�л����� 96.43% ���û�
- �ڴ�����: 33.5 MB, ������ C# �ύ�л����� 13.63% ���û�

```c
public class MinStack
{
    /** initialize your data structure here. */
    private readonly Stack<int> _stack;
    private readonly Stack<int> _stackMin;

    public MinStack()
    {
        _stack = new Stack<int>();
        _stackMin = new Stack<int>();
    }

    public void Push(int x)
    {
        _stack.Push(x);
        if (_stackMin.Count == 0 || _stackMin.Peek() >= x)
        {
            _stackMin.Push(x);
        }
    }

    public void Pop()
    {
        int x = _stack.Pop();
        if (_stackMin.Peek() == x)
        {
            _stackMin.Pop();
        }
    }

    public int Top()
    {
        return _stack.Peek();
    }

    public int GetMin()
    {
        return _stackMin.Peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.Push(x);
 * obj.Pop();
 * int param_3 = obj.Top();
 * int param_4 = obj.GetMin();
 */
```




---
## ��Ŀ02����Ч������

> - ��ţ�20
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/valid-parentheses/

����һ��ֻ���� '('��')'��'{'��'}'��'['��']' ���ַ������ж��ַ����Ƿ���Ч��

��Ч�ַ��������㣺

- �����ű�������ͬ���͵������űպϡ�
- �����ű�������ȷ��˳��պϡ�

ע����ַ����ɱ���Ϊ����Ч�ַ�����

<b>ʾ�� 1</b>:
```c
����: "()"
���: true
```

<b>ʾ�� 2</b>:
```c
����: "()[]{}"
���: true
```

<b>ʾ�� 3</b>:
```c
����: "(]"
���: false
```

<b>ʾ�� 4</b>:
```c
����: "([)]"
���: false
```

<b>ʾ�� 5</b>:
```c
����: "{[]}"
���: true
```

<b>ʾ�� 6</b>:
```c
����: ""
���: true
```



<b>ʾ�� 7</b>:
```c
����: "(("
���: false
```

**˼·**������ջ��

�����жϸ��ַ������ȵ���ż�ԣ�������������򷵻�false����������ջ�Ƚ�������ص㣬������{������[������(��������ջ������������}������]������)������ջ��Ԫ�ؽ��бȽϣ�����Ƕ�Ӧ�������ջ�����򷵻�false��

**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��88 ms, ������ C# �ύ�л����� 70.31% ���û�
- �ڴ����ģ�22 MB, ������ C# �ύ�л����� 17.91% ���û�


```c
public class Solution {
    public bool IsValid(string s) 
    {
        if (string.IsNullOrEmpty(s))
            return true;

        int count = s.Length;
        if(count%2 == 1)
            return false;
            
        Stack<char> stack = new Stack<char>();
        for (int i = 0; i < count; i++)
        {
            char c = s[i];
            if (stack.Count == 0)
            {
                stack.Push(c);
            }
            else if(c == '[' || c == '{' || c == '(')
            {
                stack.Push(c);
            }
            else if (stack.Peek() == GetPair(c))
            {
                stack.Pop();
            }
            else
            {
                return false;
            }
        }
        return stack.Count == 0;        
    }
    
    public static char GetPair(char c)
    {
        if (c == ')')
            return '(';
        if (c == '}')
            return '{';
        if (c == ']')
            return '[';
        return '\0';
    }    
}
```

---
## ��Ŀ03���ö���ʵ��ջ

> - ��ţ�225
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/implement-stack-using-queues/

ʹ�ö���ʵ��ջ�����в�����

- `push(x)` -- Ԫ�� x ��ջ
- `pop()` -- �Ƴ�ջ��Ԫ��
- `top()` -- ��ȡջ��Ԫ�ء�
- `empty()` -- ����ջ�Ƿ�Ϊ��

**ע��:**

- ��ֻ��ʹ�ö��еĻ�������-- Ҳ���� push to back, peek/pop from front, size, �� is empty ��Щ�����ǺϷ��ġ�
- ����ʹ�õ�����Ҳ��֧�ֶ��С������ʹ�� `list` ���� `deque`��˫�˶��У���ģ��һ������, ֻҪ�Ǳ�׼�Ķ��в������ɡ�
- ����Լ������в���������Ч�ģ�����, ��һ���յ�ջ������� `pop` ���� `top` ��������


**˼·**����νʵ��ջ��������ӻ����ʱѭ��ǰn-1���ڵ㣬�Ӷ��׳��Ӻ������ټ�������ڶ�β����ʵ�ֶӷ���

**�ο����룺**

- ִ�н����ͨ��
- ִ����ʱ��124 ms, ������ C# �ύ�л����� 56.21% ���û�
- �ڴ����ģ�23.4 MB, ������ C# �ύ�л����� 63.73% ���û�

```c
public class MyStack
{
    Queue<int> queue = new Queue<int>();

    /** Initialize your data structure here. */
    public MyStack()
    {
    }

    /** Push element x onto stack. */
    public void Push(int x)
    {
        queue.Enqueue(x);
        for (int i = 0; i < queue.Count - 1; i++)
        {
            queue.Enqueue(queue.Dequeue());
        }
    }

    /** Removes the element on top of the stack and returns that element. */
    public int Pop()
    {
        return queue.Count > 0 ? queue.Dequeue() : -1;
    }

    /** Get the top element. */
    public int Top()
    {
        return queue.Count > 0 ? queue.Peek() : -1;
    }

    /** Returns whether the stack is empty. */
    public bool Empty()
    {
        return queue.Count == 0;
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.Push(x);
 * int param_2 = obj.Pop();
 * int param_3 = obj.Top();
 * bool param_4 = obj.Empty();
 */
```


---
## ��Ŀ04��������ת

> - ��ţ�7
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/reverse-integer/


����һ�� 32 λ���з�������������Ҫ�����������ÿλ�ϵ����ֽ��з�ת��

<b>ʾ�� 1</b>:
```python
����: 123
���: 321
```

<b>ʾ�� 2</b>:
```python
����: -123
���: -321
```

<b>ʾ�� 3</b>:
```python
����: 120
���: 21
```
<b>ʾ�� 4</b>:
```python
����: 2147483647��2^31 ? 1 = int.MaxValue��
���: 0
```
<b>ʾ�� 5</b>:
```python
����: -2147483648��?2^31 = int.MinValue��
���: 0
```


<b>ע��</b>��

�������ǵĻ���ֻ�ܴ洢���� 32 λ���з���������������ֵ��ΧΪ`[?2^31, 2^31 ? 1]`�������������裬�����ת�����������ô�ͷ��� 0��


**˼·**��ͨ�����еķ�ʽ���Ѹ���ת��Ϊ������ͨ�������С�ͳһ����

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 56 ms, ������ C# �ύ�л����� 93.28% ���û�
- �ڴ�����: 13.9 MB, ������ C# �ύ�л����� 13.98% ���û�

```c
public class Solution {
    public int Reverse(int x) {
        if (x == int.MinValue)
            return 0;

        long result = 0;
        int negative = x < 0 ? -1 : 1;
        x = negative * x;

        Queue<int> q = new Queue<int>();
        while (x != 0)
        {
            q.Enqueue(x % 10);
            x = x/10;
        }
            
        while (q.Count != 0)
        {
            result += q.Dequeue()*(long) Math.Pow(10, q.Count);
            if (negative == 1 && result > int.MaxValue)
            {
                result = 0;
                break;
            }
            if (negative == -1 && result*-1 < int.MinValue)
            {
                result = 0;
                break;
            }
        }
        return (int)result*negative;        
    }
}
```

---
## ��Ŀ05���沨�����ʽ��ֵ

> - ��ţ�150
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/

�����沨����ʾ��������ʽ��ֵ��

��Ч����������� +, -, *, / ��ÿ��������������������Ҳ��������һ���沨�����ʽ��

˵����

- ��������ֻ�����������֡�
- �����沨�����ʽ������Ч�ġ����仰˵�����ʽ�ܻ�ó���Ч��ֵ�Ҳ����ڳ���Ϊ 0 �������

<b>ʾ�� 1</b>��

```c
����: ["2", "1", "+", "3", "*"]
���: 9
����: ((2 + 1) * 3) = 9
```

<b>ʾ�� 2</b>��

```c
����: ["4", "13", "5", "/", "+"]
���: 6
����: (4 + (13 / 5)) = 6
```

<b>ʾ�� 3</b>��

```c
����: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
���: 22
����: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```



**˼·**������ջ����ȳ������Խ����㷨�����ʵ�֡�

**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��100 ms, ������ C# �ύ�л����� 100.00% ���û�
- �ڴ����ģ�25 MB, ������ C# �ύ�л����� 69.81% ���û�

```c
public class Solution {
    public int EvalRPN(string[] tokens) 
    {
        Stack<int> stack = new Stack<int>();
        for (int i = 0; i < tokens.Length; i++)
        {
            string str = tokens[i];
            if (str == "+" || str == "-" || str == "*" || str == "/")
            {
                int b = stack.Pop();
                int a = stack.Pop();
                int c = Compute(a, b, str);
                stack.Push(c);
            }
            else
            {
                stack.Push(int.Parse(str));
            }
        }
        return stack.Pop();        
    }
    
    public static int Compute(int a, int b, string oper)
    {
        int result = 0;
        switch (oper)
        {
            case "+":
                result = a + b;
                break;
            case "-":
                result = a - b;
                break;
            case "*":
                result = a * b;
                break;
            case "/":
                result = a / b;
                break;
        }
        return result;
    }    
}
```


---
## ��Ŀ06��ȫ����

> - ��ţ�46
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/permutations/

����һ��û���ظ����ֵ����У����������п��ܵ�ȫ���С�

<b>ʾ��</b>:
```c
����: [1,2,3]
���:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```



<b>˼·�����ݷ���back tracking��</b> ��һ��ѡ�����������ֳ�Ϊ��̽������ѡ��������ǰ�������ԴﵽĿ�ꡣ����̽����ĳһ��ʱ������ԭ��ѡ�񲢲��Ż�ﲻ��Ŀ�꣬���˻�һ������ѡ�������߲�ͨ���˻����ߵļ���Ϊ���ݷ������������������ĳ��״̬�ĵ��Ϊ�����ݵ㡱��

> �׻������ݷ��������Ϊͨ��ѡ��ͬ�Ĳ�·��Ѱ��Ŀ�ĵأ�һ����·��һ����·�ڵ�ȥ�����ҵ�Ŀ�ĵء�����ߴ���·�������������ҵ���·�ڵ���һ��·��ֱ���ҵ�Ŀ�ĵء�

����ϰ�Ļ��ݹ���������ʾ��


![���ݹ���](https://img-blog.csdnimg.cn/20201009214444744.png)

**�ο����룺**

- ״̬��ͨ��
- ִ����ʱ: 364 ms, ������ C# �ύ�л����� 80.00% ���û�
- �ڴ�����: 30.6 MB, ������ C# �ύ�л����� 7.14% ���û�

```c
public class Solution
{
    private IList<IList<int>> _result;
    private bool[] _used;

    public IList<IList<int>> Permute(int[] nums)
    {
        _result = new List<IList<int>>();
        if (nums == null || nums.Length == 0)
            return _result;
        _used = new bool[nums.Length];

        FindPath(nums, 0, new List<int>());
        return _result;
    }

    public void FindPath(int[] nums, int count, List<int> path)
    {
        if (count == nums.Length)
        {
            //�ݹ���ֹ����
            List<int> item = new List<int>();
            item.AddRange(path);
            //���뿽��
            _result.Add(item);
            return;
        }
        for (int i = 0; i < nums.Length; i++)
        {
            if (_used[i] == false)
            {
                path.Add(nums[i]);
                _used[i] = true;
                FindPath(nums, count + 1, path);
                path.RemoveAt(path.Count - 1);
                _used[i] = false;
            }
        }
    }
}
```




---
## ��Ŀ07���ַ���ת������ (atoi)

> - ��ţ�8
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/string-to-integer-atoi/

������ʵ��һ�� `atoi` ������ʹ���ܽ��ַ���ת����������

���ȣ��ú����������Ҫ�������õĿ�ͷ�ո��ַ���ֱ��Ѱ�ҵ���һ���ǿո���ַ�Ϊֹ��

������Ѱ�ҵ��ĵ�һ���ǿ��ַ�Ϊ�����߸���ʱ���򽫸÷�����֮���澡���ܶ���������������������Ϊ�������������ţ������һ���ǿ��ַ������֣���ֱ�ӽ�����֮�������������ַ�����������γ�������

���ַ���������Ч����������֮��Ҳ���ܻ���ڶ�����ַ�����Щ�ַ����Ա����ԣ����Ƕ��ں�����Ӧ�����Ӱ�졣

ע�⣺������ַ����еĵ�һ���ǿո��ַ�����һ����Ч�����ַ����ַ���Ϊ�ջ��ַ����������հ��ַ�ʱ������ĺ�������Ҫ����ת����

���κ�����£����������ܽ�����Ч��ת��ʱ���뷵�� 0��

<b>˵��</b>��

�������ǵĻ���ֻ�ܴ洢 32 λ��С���з�����������ô����ֵ��ΧΪ `[?2^31, 2^31? 1]`�������ֵ���������Χ���뷵�� `INT_MAX (2^31? 1)` �� `INT_MIN (?2^31)` ��

<b>ʾ�� 1</b>:
```c
����: "42"
���: 42
```

<b>ʾ�� 2</b>:
```c
����: "   -42"
���: -42
����: ��һ���ǿհ��ַ�Ϊ '-', ����һ�����š�
���Ǿ����ܽ���������������������ֵ�����������������õ� -42 ��
```
<b>ʾ�� 3</b>:
```c
����: "4193 with words"
���: 4193
����: ת����ֹ������ '3' ����Ϊ������һ���ַ���Ϊ���֡�
```

<b>ʾ�� 4</b>:
```c
����: "words and 987"
���: 0
����: ��һ���ǿ��ַ��� 'w', �����������ֻ��������š�
����޷�ִ����Ч��ת����
```

<b>ʾ�� 5</b>:
```c
����: "-91283472332"
���: -2147483648
����: ���� "-91283472332" ���� 32 λ�з���������Χ�� 
��˷��� INT_MIN (?231) ��
```


<b>ʾ�� 6</b>:
```c
����: "  0000000000012345678"
���: 12345678
```

<b>ʾ�� 7</b>:
```c
����: "20000000000000000000"
���: 2147483647
```

**˼·**��ͨ�����еķ�ʽ��

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 104 ms, ������ C# �ύ�л����� 98.32% ���û�
- �ڴ�����: 24.3 MB, ������ C# �ύ�л����� 24.45% ���û�

```c
public class Solution {
    public int MyAtoi(string str) {
        str = str.Trim();
        if (string.IsNullOrEmpty(str))
            return 0;

        if (str[0] != '-' && str[0] != '+')
        {
            if (str[0] < '0' || str[0] > '9')
                return 0;
        }
        int negative = 1;
        long result = 0;
        Queue<int> q = new Queue<int>();
        for (int i = 0; i < str.Length; i++)
        {
            if (str[i] == '-' && i == 0)
            {
                negative = -1;
                continue;
            }
            if (str[i] == '+' && i == 0)
            {
                continue;
            }
            if (str[i] < '0' || str[i] > '9')
            {
                break;
            }
            q.Enqueue(str[i] - '0');
        }

        while (q.Count != 0)
        {
            int i = q.Dequeue();

            //ȥ������ǰ�˵���
            if (i == 0 && result == 0)
                continue;
                
            // ���س���λ��������
            if (negative == 1 && q.Count > 10)
            {
                return int.MaxValue;
            }
            if (negative == -1 && q.Count > 10)
            {
                return int.MinValue;
            }

            result += i * (long)Math.Pow(10, q.Count);
            if (negative == 1 && result > int.MaxValue)
            {
                return int.MaxValue;
            }
            if (negative == -1 && result * -1 < int.MinValue)
            {
                return int.MinValue;
            }
        }
        return (int)result * negative;        
    }
}
```

---
## ��Ŀ08�����ѭ��˫�˶���

> - ��ţ�641
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/design-circular-deque/

���ʵ��˫�˶��С�

���ʵ����Ҫ֧�����²�����

- `MyCircularDeque(k)`�����캯��,˫�˶��еĴ�СΪk��
- `insertFront()`����һ��Ԫ����ӵ�˫�˶���ͷ���� ��������ɹ����� true��
- `insertLast()`����һ��Ԫ����ӵ�˫�˶���β������������ɹ����� true��
- `deleteFront()`����˫�˶���ͷ��ɾ��һ��Ԫ�ء� ��������ɹ����� true��
- `deleteLast()`����˫�˶���β��ɾ��һ��Ԫ�ء���������ɹ����� true��
- `getFront()`����˫�˶���ͷ�����һ��Ԫ�ء����˫�˶���Ϊ�գ����� -1��
- `getRear()`�����˫�˶��е����һ��Ԫ�ء����˫�˶���Ϊ�գ����� -1��
- `isEmpty()`�����˫�˶����Ƿ�Ϊ�ա�
- `isFull()`�����˫�˶����Ƿ����ˡ�

<b>ʾ��</b>��

```c
MyCircularDeque circularDeque = new MycircularDeque(3); // ����������СΪ3
circularDeque.insertLast(1);			        // ���� true
circularDeque.insertLast(2);			        // ���� true
circularDeque.insertFront(3);			        // ���� true
circularDeque.insertFront(4);			        // �Ѿ����ˣ����� false
circularDeque.getRear();  				// ���� 2
circularDeque.isFull();				        // ���� true
circularDeque.deleteLast();			        // ���� true
circularDeque.insertFront(4);			        // ���� true
circularDeque.getFront();				// ���� 4
```

<b>��ʾ</b>��

- ����ֵ�ķ�ΧΪ [1, 1000]
- ���������ķ�ΧΪ [1, 1000]
- �벻Ҫʹ�����õ�˫�˶��п⡣


**�ο�����**��

- ִ�н����ͨ��
- ִ����ʱ��160 ms, ������ C# �ύ�л����� 90.48% ���û�
- �ڴ����ģ�34.7 MB, ������ C# �ύ�л����� 7.14% ���û�


```c
public class MyCircularDeque 
{
    private int _pFront;
    private int _pRear;
    private readonly int[] _dataset;
    private int _length;
    private int _maxSize;
    
    /** Initialize your data structure here. Set the size of the deque to be k. */
    public MyCircularDeque(int k) 
    {
        _dataset = new int[k];
        _length = 0;
        _maxSize = k;
        _pFront = 0;
        _pRear = 0;        
    }
    
    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    public bool InsertFront(int value) 
    {
        if (_length == _maxSize)
            return false;

        _pFront = (_pFront - 1 + _maxSize)%_maxSize;
        _dataset[_pFront] = value;
        _length++;
        return true;        
    }
    
    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    public bool InsertLast(int value) 
    {
        if (_length == _maxSize)
            return false;

        _dataset[_pRear] = value;
        _pRear = (_pRear + 1)%_maxSize;
        _length++;
        return true;        
    }
    
    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    public bool DeleteFront() 
    {
        if (_length == 0)
            return false;
        _pFront = (_pFront + 1)%_maxSize;
        _length--;
        return true;        
    }
    
    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    public bool DeleteLast() 
    {
        if (_length == 0)
            return false;
        _pRear = (_pRear - 1 + _maxSize)%_maxSize;
        _length--;
        return true;        
    }
    
    /** Get the front item from the deque. */
    public int GetFront() 
    {
        if (_length == 0)
            return -1;

        return _dataset[_pFront];        
    }
    
    /** Get the last item from the deque. */
    public int GetRear() 
    {
        if (_length == 0)
            return -1;
        int index = (_pRear - 1 + _maxSize)%_maxSize;
        return _dataset[index];        
    }
    
    /** Checks whether the circular deque is empty or not. */
    public bool IsEmpty() 
    {
        return _length == 0;        
    }
    
    /** Checks whether the circular deque is full or not. */
    public bool IsFull() 
    {
        return _length == _maxSize;        
    }
}

/**
 * Your MyCircularDeque object will be instantiated and called as such:
 * MyCircularDeque obj = new MyCircularDeque(k);
 * bool param_1 = obj.InsertFront(value);
 * bool param_2 = obj.InsertLast(value);
 * bool param_3 = obj.DeleteFront();
 * bool param_4 = obj.DeleteLast();
 * int param_5 = obj.GetFront();
 * int param_6 = obj.GetRear();
 * bool param_7 = obj.IsEmpty();
 * bool param_8 = obj.IsFull();
 */
```





---
## ��Ŀ09�����Ч����

> - ��ţ�32
> - �Ѷȣ�����
> - https://leetcode-cn.com/problems/longest-valid-parentheses/

����һ��ֻ���� '(' �� ')' ���ַ������ҳ���İ�����Ч���ŵ��Ӵ��ĳ��ȡ�

<b>ʾ�� 1</b>:

```c
����: "(()"
���: 2
����: ���Ч�����Ӵ�Ϊ "()"
```

<b>ʾ�� 2</b>:
```c
����: ")()())"
���: 4
����: ���Ч�����Ӵ�Ϊ "()()"
```

<b>ʾ�� 3</b>:
```c
����: ""
���: 0
����: 
```
<b>ʾ�� 4</b>:
```c
����: "()(())"
���: 6
����: ���Ч�����Ӵ�Ϊ "()(())"
```

**˼·**������ջ��

���ǿ�����ջ�ڱ��������ַ����Ĺ�����ȥ�жϵ�ĿǰΪֹɨ������ַ�������Ч�ԣ�ͬʱ�������Ч�ַ����ĳ��ȡ��������Ƚ� ?1 ����ջ����

- ����������ÿ����(�������ǽ������±����ջ�С�
- ����������ÿ����)�������ǵ���ջ����Ԫ�أ��ж���Ч�ԣ�������Ч���ȡ�

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ��92 ms, ������ C# �ύ�л����� 53.78% ���û�
- �ڴ����ģ�23.5 MB, ������ C# �ύ�л����� 7.14% ���û�

```c
public class Solution {
    public int LongestValidParentheses(string s) {
        Stack<int> stack = new Stack<int>();
        stack.Push(-1);
        int result = 0;
        for (int i = 0; i < s.Length; i++)
        {
            if (s[i] == '(')
            {
                stack.Push(i);
            }
            else
            {
                stack.Pop();
                if (stack.Count == 0)
                {
                    stack.Push(i);
                }
                else
                {
                    result = Math.Max(result, i - stack.First());
                }
            }
        }
        return result;
    }
}
```

---
## ��Ŀ10�������������ֵ

> - ��ţ�239
> - �Ѷȣ�����
> - https://leetcode-cn.com/problems/sliding-window-maximum/

����һ������ nums����һ����СΪ k �Ļ������ڴ������������ƶ�����������Ҳࡣ��ֻ���Կ����ڻ��������ڵ� k �����֡���������ÿ��ֻ�����ƶ�һλ��

���ػ��������е����ֵ��

<b>ʾ��</b>:

```c
����: nums = [1,3,-1,-3,5,3,6,7], �� k = 3
���: [3,3,5,5,6,7] 
����: 

  �������ڵ�λ��                ���ֵ
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

<b>��ʾ</b>��

����Լ��� k ������Ч�ģ����������鲻Ϊ�յ�����£�1 �� k �� ��������Ĵ�С��

 

<b>����</b>��

����������ʱ�临�Ӷ��ڽ��������

**�ο����룺**

<b>ʵ��һ</b>������Ѱ��ÿ�����ڵ����ֵ��


- ״̬��ͨ��
- ִ����ʱ: 472 ms, ������ C# �ύ�л����� 53.33% ���û�
- �ڴ�����: 34.3 MB, ������ C# �ύ�л����� 50.00% ���û�

```c
public class Solution {
    public int[] MaxSlidingWindow(int[] nums, int k) {
        int len = nums.Length;
        if (len == 0)
            return nums;

        int[] result = new int[len - k + 1];
        for (int i = 0; i < result.Length; i++)
        {
            result[i] = GetMax(nums, i, i + k);
        }
        return result;        
    }
    
    public int GetMax(int[] arr,int start,int end)
    {
        int max = int.MinValue;
        for (int i = start; i < end; i++)
        {
            if (arr[i] > max)
                max = arr[i];
        }
        return max;
    }    
}
```

<b>ʵ�ֶ�</b>�����������ʱ��Ч�ʾ���Ҫʹ�ýṹ�ˡ�

- ״̬��ͨ��
- ִ����ʱ: 364 ms, ������ C# �ύ�л����� 75.33% ���û�
- �ڴ�����: 40.5 MB, ������ C# �ύ�л����� 100.00% ���û�


**˼·**������ѭ��˫�˶�������¼��ǰ���ڵ���Ϣ�����д��������ֵ������λ�ü�¼�ڶ���Ԫ���С���˫�˶���Ҫ��֤����������λ�õ���ֵ�ɴ�С����
- ������������Ҫɾ������Ԫ�ء�
- ���ڶ�βԪ�أ�Ҫ����ɾ����βԪ�أ��Ѹ�Ԫ�ص�λ�ò��뵽��β��


```c
public class MyCircularDeque
{
    private int _pFront;
    private int _pRear;
    private readonly int[] _dataset;
    private int _length;
    private int _maxSize;

    /** Initialize your data structure here. Set the size of the deque to be k. */
    public MyCircularDeque(int k)
    {
        _dataset = new int[k];
        _length = 0;
        _maxSize = k;
        _pFront = 0;
        _pRear = 0;
    }

    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    public bool InsertFront(int value)
    {
        if (_length == _maxSize)
            return false;

        _pFront = (_pFront - 1 + _maxSize) % _maxSize;
        _dataset[_pFront] = value;
        _length++;
        return true;
    }

    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    public bool InsertLast(int value)
    {
        if (_length == _maxSize)
            return false;

        _dataset[_pRear] = value;
        _pRear = (_pRear + 1) % _maxSize;
        _length++;
        return true;
    }

    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    public bool DeleteFront()
    {
        if (_length == 0)
            return false;
        _pFront = (_pFront + 1) % _maxSize;
        _length--;
        return true;
    }

    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    public bool DeleteLast()
    {
        if (_length == 0)
            return false;
        _pRear = (_pRear - 1 + _maxSize) % _maxSize;
        _length--;
        return true;
    }

    /** Get the front item from the deque. */
    public int GetFront()
    {
        if (_length == 0)
            return -1;

        return _dataset[_pFront];
    }

    /** Get the last item from the deque. */
    public int GetRear()
    {
        if (_length == 0)
            return -1;
        int index = (_pRear - 1 + _maxSize) % _maxSize;
        return _dataset[index];

    }

    /** Checks whether the circular deque is empty or not. */
    public bool IsEmpty()
    {
        return _length == 0;
    }

    /** Checks whether the circular deque is full or not. */
    public bool IsFull()
    {
        return _length == _maxSize;
    }
}

public class Solution {
    public int[] MaxSlidingWindow(int[] nums, int k) {
        int len = nums.Length;
        if (len == 0)
            return nums;
        int[] result = new int[len - k + 1];
        MyCircularDeque deque = new MyCircularDeque(k);

        for (int i = 0; i < len; i++)
        {
            // �жϵ�ǰ�����ж��׵�ֵ�Ƿ���Ч
            if (deque.IsEmpty() == false && deque.GetFront() <= i - k)
            {
                deque.DeleteFront();
            }

            // ��֤�Ӵ�С ���ǰ����С����Ҫ���ε�����ֱ������Ҫ��
            while (deque.IsEmpty() == false && nums[deque.GetRear()] <= nums[i])
            {
                deque.DeleteLast();
            }
            //��ӵ�ǰֵ��Ӧ�������±�
            deque.InsertLast(i);

            // �����ڳ���Ϊkʱ ���浱ǰ���������ֵ
            if (i + 1 >= k)
            {
                result[i + 1 - k] = nums[deque.GetFront()];
            }
        }
        return result;        
    }
}
```

---
<p style="text-align:center;">
<img src="https://img-blog.csdnimg.cn/20200727174102237.png">
</p>