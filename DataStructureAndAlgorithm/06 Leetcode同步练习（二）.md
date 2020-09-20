
# Leetcodeͬ����ϰ������

## ��Ŀ01��������

> - ��ţ�9
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/palindrome-number/

�ж�һ�������Ƿ��ǻ���������������ָ���򣨴������ң��͵��򣨴������󣩶�����һ����������

<b>ʾ�� 1</b>:
```c
����: 121
���: true
```

<b>ʾ�� 2</b>:

```c
����: -121
���: false
����: �������Ҷ�, Ϊ -121 �� ���������, Ϊ 121- �����������һ����������
```

<b>ʾ�� 3</b>:
```c
����: 10
���: false
����: ���������, Ϊ 01 �����������һ����������
```

<b>����</b>:

���ܲ�������תΪ�ַ�����������������

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 76 ms, ������ C# �ύ�л����� 98.90% ���û�
- �ڴ�����: 14.9 MB, ������ C# �ύ�л����� 85.12% ���û�

```c
public class Solution {
    public bool IsPalindrome(int x) {
        if (x < 0)
            return false;

        int bit = 1;
        while (x / bit >= 10)
        {
            bit = bit * 10;
        }

        while (x > 0)
        {
            int left = x % 10;
            int right = x / bit;
            if (left != right)
            {
                return false;
            }
            x = (x % bit) / 10;
            bit = bit / 100;
        }
        return true;
}
```



---
## ��Ŀ02��x ��ƽ����

> - ��ţ�69
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/sqrtx/

ʵ�� `int sqrt(int x)` ������

���㲢����`x`��ƽ����������`x`�ǷǸ�������

���ڷ������������������ֻ���������Ĳ��֣�С�����ֽ�����ȥ��

<b>ʾ�� 1</b>:

```c
����: 4
���: 2
```

<b>ʾ�� 2</b>:

```c
����: 8
���: 2
˵��: 8 ��ƽ������ 2.82842..., ���ڷ���������������С�����ֽ�����ȥ��
```

**˼·**������ţ�ٵ�������

![ţ�ٵ�����ʽ](https://img-blog.csdnimg.cn/2019082111485172.png)


**�ο�����**

- ״̬��ͨ��
- ִ����ʱ: 48 ms, ������ C# �ύ�л����� 100.00% ���û�
- �ڴ�����: 13.7 MB, ������ C# �ύ�л����� 5.40% ���û�

```c
public class Solution {
    public int MySqrt(int x) {
        if (x < 0)
            throw new ArgumentOutOfRangeException();

        double error = 1.0e-5;
        double cur = x;
        while (Math.Abs(cur*cur - x) > error)
        {
            cur = (cur + 1.0*x/cur)/2.0;
        }
        return (int)cur;        
    }
}
```


---
## ��Ŀ03����¥��

> - ��ţ�70
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/climbing-stairs/

������������¥�ݡ���Ҫ n ������ܵ���¥����

ÿ��������� 1 �� 2 ��̨�ס����ж����ֲ�ͬ�ķ�����������¥���أ�

<b>ע��</b>������ n ��һ����������

<b>ʾ�� 1</b>��
```c
���룺 2
����� 2
���ͣ� �����ַ�����������¥����
1.  1 �� + 1 ��
2.  2 ��
```

<b>ʾ�� 2</b>��
```c
���룺 3
����� 3
���ͣ� �����ַ�����������¥����
1.  1 �� + 1 �� + 1 ��
2.  1 �� + 2 ��
3.  2 �� + 1 ��
```

<b>ʾ�� 3</b>��
```c
���룺 44
����� 1134903170
```

**˼·**������ѭ��

���������Ŀ��
- 1 �ף�f(1) = 1 �ַ���
- 2 �ף�f(2) = 2 �ַ���
- 3 �ף�f(3) = 3 �ַ���
- 4 �ף�f(4) = 5 �ַ���
- ����
- n �ף�f(n) = f(n-1) + f(n-2) �ַ���

�������������ת��Ϊ쳲������������⡣

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 52 ms, ������ C# �ύ�л����� 97.87% ���û�
- �ڴ�����: 13.7 MB, ������ C# �ύ�л����� 5.98% ���û�

```c
public class Solution {
    public int ClimbStairs(int n) {
        if (n <= 2)
            return n;

        int first = 1;
        int second = 2;
        int result = 0;

        for (int i = 3; i <= n; i++)
        {
            result = first + second;
            first = second;
            second = result;
        }
        return result;        
    }
}
```

---
## ��Ŀ04��������Ʊ�����ʱ��

> - ��ţ�121
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/

����һ�����飬���ĵ� i ��Ԫ����һ֧������Ʊ�� i ��ļ۸�

��������ֻ�������һ�ʽ��ף������������һ֧��Ʊ�������һ���㷨�����������ܻ�ȡ���������

ע���㲻���������Ʊǰ������Ʊ��

<b>ʾ�� 1</b>:
```c
����: [7,1,5,3,6,4]
���: 5
����: �ڵ� 2 �죨��Ʊ�۸� = 1����ʱ�����룬�ڵ� 5 �죨��Ʊ�۸� = 6����ʱ��������������� = 6-1 = 5 ��
     ע���������� 7-1 = 6, ��Ϊ�����۸���Ҫ��������۸�
```

<b>ʾ�� 2</b>:
```c
����: [7,6,4,3,1]
���: 0
����: �����������, û�н������, �����������Ϊ 0��
```

**˼·**���������ѹ�Ʊ�����ܹ�׬���Ǯ�����ֵ����Ϊ�������


**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 132 ms, ������ C# �ύ�л����� 97.33% ���û�
- �ڴ�����: 24 MB, ������ C# �ύ�л����� 5.62% ���û�

```c
public class Solution
{
    public int MaxProfit(int[] prices)
    {
        if (prices.Length <= 1)
            return 0;

        int min = prices[0];
        int max = 0;
        for (int i = 1; i < prices.Length; i++)
        {
            int earn = prices[i] - min;
            if (earn > max)
            {
                max = earn;
            }
            if (prices[i] < min)
            {
                min = prices[i];
            }
        }
        return max;
    }
}
```


---
## ��Ŀ05��������Ʊ�����ʱ�� II

> - ��ţ�122
> - �Ѷȣ���
> - https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/


����һ�����飬���ĵ� i ��Ԫ����һ֧������Ʊ�� i ��ļ۸�

���һ���㷨�����������ܻ�ȡ�������������Ծ����ܵ���ɸ���Ľ��ף��������һ֧��Ʊ����

<b>ע��</b>���㲻��ͬʱ�����ʽ��ף���������ٴι���ǰ���۵�֮ǰ�Ĺ�Ʊ����

<b>ʾ�� 1</b>:
```c
����: [7,1,5,3,6,4]
���: 7
����: 
    �ڵ� 2 �죨��Ʊ�۸� = 1����ʱ�����룬�ڵ� 3 �죨��Ʊ�۸� = 5����ʱ������, ��ʽ������ܻ������ = 5-1 = 4 ��
    ����ڵ� 4 �죨��Ʊ�۸� = 3����ʱ�����룬�ڵ� 5 �죨��Ʊ�۸� = 6����ʱ������, ��ʽ������ܻ������ = 6-3 = 3 ��
```

<b>ʾ�� 2</b>:
```c
����: [1,2,3,4,5]
���: 4
����: 
    �ڵ� 1 �죨��Ʊ�۸� = 1����ʱ�����룬�ڵ� 5 �� ����Ʊ�۸� = 5����ʱ������, ��ʽ������ܻ������ = 5-1 = 4 ��
    ע���㲻���ڵ� 1 ��͵� 2 ����������Ʊ��֮���ٽ�����������
    ��Ϊ��������ͬʱ�����˶�ʽ��ף���������ٴι���ǰ���۵�֮ǰ�Ĺ�Ʊ��
```
    
<b>ʾ�� 3</b>:
```c
����: [7,6,4,3,1]
���: 0
����: �����������, û�н������, �����������Ϊ 0��
```

**˼·**��̰���㷨

̰�Ĳ��ԣ�ֻҪ��һ��۸��ǰһ��ߣ�����ǰһ�������һ��������

![�����н������](https://img-blog.csdnimg.cn/20190914100650406.png)


![�������������](https://img-blog.csdnimg.cn/20200325110545912.png)

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 140 ms, ������ C# �ύ�л����� 72.02% ���û�
- �ڴ�����: 24.2 MB, ������ C# �ύ�л����� 5.36% ���û�


```c
public class Solution
{
    public int MaxProfit(int[] prices)
    {
        int earn = 0;
        for (int i = 0; i < prices.Length-1; i++)
        {
            earn += Math.Max(prices[i + 1] - prices[i], 0);
        }
        return earn;
    }
}
```


---
## ��Ŀ06����Ծ��Ϸ

> - ��ţ�55
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/jump-game/

����һ���Ǹ��������飬�����λ������ĵ�һ��λ�á�

�����е�ÿ��Ԫ�ش������ڸ�λ�ÿ�����Ծ����󳤶ȡ�

�ж����Ƿ��ܹ��������һ��λ�á�

**ʾ�� 1:**

```c
����: [2,3,1,1,4]
���: true
����: ���ǿ������� 1 ������λ�� 0 ���� λ�� 1, Ȼ���ٴ�λ�� 1 �� 3
���������һ��λ�á�
```

**ʾ�� 2:**

```c
����: [3,2,1,0,4]
���: false
����: �������������ܻᵽ������Ϊ 3 ��λ�á�����λ�õ������Ծ������ 0��
��������Զ�����ܵ������һ��λ�á�
```

**ʾ�� 3:**

```c
���룺[0]
�����true
```

**˼·��̰���㷨**

̰�Ĳ��ԣ�ÿ�μ�¼������������ֵ�������ǰ�㳬�����ֵ������false��������ֵ�ﵽ���һ��λ�ã�����true��

**�ο����룺**

- ִ�н����ͨ��
- ִ����ʱ��120 ms, ������ C# �ύ�л����� 57.32% ���û�
- �ڴ����ģ�26.2 MB, ������ C# �ύ�л����� 6.67% ���û�

```c
public class Solution
{
    public bool CanJump(int[] nums)
    {
        int maxlength = 0;      //��¼���ܵ������Զ��
        for (int i = 0; maxlength < nums.Length-1; i++)
        {
            if (i > maxlength)
            {
                return false;//���˵��Ѳ��ܵ������false 
            }
            maxlength = Math.Max(i + nums[i], maxlength);
        }
        return true;
    }
}
```





---
## ��Ŀ07������֮��

> - ��ţ�15
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/3sum/

����һ������`n`������������`nums`���ж�`nums`���Ƿ��������Ԫ��`a��b��c`��ʹ��`a + b + c = 0`���ҳ��������������Ҳ��ظ�����Ԫ�顣

ע�⣺���в����԰����ظ�����Ԫ�顣

**ʾ����**

```c
�������� nums = [-1, 0, 1, 2, -1, -4]��

����Ҫ�����Ԫ�鼯��Ϊ��
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```



**˼·������ ���� + ������ �ķ�����**

Ϊ�˱�������ѭ��������ִ��Ч�ʡ����ȣ���`nums`��������Ȼ�󣬹̶�3������`i,l(left),r(right)`��`i`���������ѭ����`l`ָ��`nums[i]`֮���������Сֵ��`r`ָ��`nums[i]`֮����������ֵ��ģ�¿��������˼·�����`nums[i] > 0`�Ͳ���Ҫ���������ˣ��������`nums[i] + nums[l] + nums[r]`�Ƿ�����㲢������Ӧ�Ĵ�����������㣬��`l`�����ƶ�`r`ָ�룬���С���㣬��`r`�����ƶ�`l`��������������㣬����뵽�洢�������result�����С���Ȼ����Ŀ��Ҫ�������Ԫ�鲻���ظ��������ڽ��еĹ����м���ȥ�ؾͺá�

**�ο����룺**

- ִ�н����ͨ��
- ִ����ʱ��348 ms, ������ C# �ύ�л����� 99.54% ���û�
- �ڴ����ģ�35.8 MB, ������ C# �ύ�л����� 6.63% ���û�

```c
public class Solution 
{
    public IList<IList<int>> ThreeSum(int[] nums) 
    {
        IList<IList<int>> result = new List<IList<int>>();

        nums = nums.OrderBy(a => a).ToArray();
        int len = nums.Length;
        
        for (int i = 0; i < len - 2; i++)
        {
            if (nums[i] > 0) 
                break; // �����С�����ִ���0, ����Ĳ����Ѿ�û������

            if (i > 0 && nums[i - 1] == nums[i])
                continue; // ������Ԫ���е�һ��Ԫ�ص��ظ�����

            int l = i + 1;
            int r = len - 1;

            while (l < r)
            {
                int sum = nums[i] + nums[l] + nums[r];
                if (sum < 0)
                {
                    l++;
                }
                else if (sum > 0)
                {
                    r--;
                }
                else
                {
                    result.Add(new List<int>() {nums[i], nums[l], nums[r]});
                    // ������Ԫ���еڶ���Ԫ�ص��ظ�����
                    while (l < r && nums[l] == nums[l + 1]) 
                    {
                        l++;
                    }
                    // ������Ԫ���е�����Ԫ�ص��ظ�����
                    while (l < r && nums[r - 1] == nums[r]) 
                    {
                        r--;
                    }
                    l++;
                    r--;
                }
            }
        }
        return result;    
    }
}
```


---
## ��Ŀ08����ӽ�������֮��

> - ��ţ�16
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/3sum-closest/

����һ������`n`������������`nums`��һ��Ŀ��ֵ`target`���ҳ�`nums`�е�����������ʹ�����ǵĺ���`target`��ӽ����������������ĺ͡��ٶ�ÿ������ֻ����Ψһ�𰸡�

<b>ʾ��</b> :

```c
���磬�������� nums = [-1��2��1��-4], �� target = 1.
�� target ��ӽ����������ĺ�Ϊ 2. (-1 + 2 + 1 = 2).
```


<b>˼·������ ���� + ������ �ķ���</b>


**�ο����룺**

- ״̬��ͨ��
- ִ����ʱ: 132 ms, ������ C# �ύ�л����� 100.00% ���û�
- �ڴ�����: 24 MB, ������ C# �ύ�л����� 5.55% ���û�


```c
public class Solution 
{
    public int ThreeSumClosest(int[] nums, int target) 
    {
        nums = nums.OrderBy(a => a).ToArray();
        int result = nums[0] + nums[1] + nums[2];
        for (int i = 0; i < nums.Length - 2; i++)
        {
            int start = i + 1, end = nums.Length - 1;
            while (start < end)
            {
                int sum = nums[start] + nums[end] + nums[i];
                if (Math.Abs(target - sum) < Math.Abs(target - result))
                    result = sum;
                if (sum > target)
                    end--;
                else if (sum < target)
                    start++;
                else
                    return result;
            }
        }
        return result;        
    }
}
```

---
## ��Ŀ09���������� II

> - ��ţ�59
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/spiral-matrix-ii/

����һ�������� n������һ������ 1 �� n^2 ����Ԫ�أ���Ԫ�ذ�˳ʱ��˳���������е������ξ���

<b>ʾ��</b>:
```c
����: 3
���:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

**�ο�����**��

- ״̬��ͨ��
- ִ����ʱ: 296 ms, ������ C# �ύ�л����� 97.67% ���û�
- �ڴ�����: 25 MB, ������ C# �ύ�л����� 11.11% ���û�

```c
public class Solution
{
    public int[][] GenerateMatrix(int n)
    {
        int[][] matrix = new int[n][];
        for (int i = 0; i < n; i++)
        {
            matrix[i] = new int[n];
        }

        int start = 0;//��ʼλ��
        int end1 = n - 1;//�����λ��
        int end2 = n - 1;//���±�λ��
        int count = 1;

        while (start < end1 && start < end2)
        {
            LeftToRight(start, end1, start, matrix, ref count);
            TopToBottom(start + 1, end2, end1, matrix, ref count);
            RightToLeft(end1 - 1, start, end2, matrix, ref count);
            BottomToTop(end2 - 1, start + 1, start, matrix, ref count);
            start++;
            end1 = n - 1 - start;
            end2 = n - 1 - start;
        }
        if (n%2 == 1)
        {
            matrix[start][start] = count;
        }
        return matrix;
    }

    private void LeftToRight(int start, int end, int rowIndex, int[][] matrix, ref int from)
    {
        for (int i = start; i <= end; i++)
        {
            matrix[rowIndex][i] = from;
            from++;
        }
    }

    private void TopToBottom(int start, int end, int colIndex, int[][] matrix, ref int from)
    {
        for (int i = start; i <= end; i++)
        {
            matrix[i][colIndex] = from;
            from++;
        }
    }

    private void RightToLeft(int start, int end, int rowIndex, int[][] matrix, ref int from)
    {
        for (int i = start; i >= end; i--)
        {
            matrix[rowIndex][i] = from;
            from++;
        }
    }

    private void BottomToTop(int start, int end, int colIndex, int[][] matrix, ref int from)
    {
        for (int i = start; i >= end; i--)
        {
            matrix[i][colIndex] = from;
            from++;
        }
    }
}
```



## ��Ŀ10����ͬ·��

> - ��ţ�62
> - �Ѷȣ��е�
> - https://leetcode-cn.com/problems/unique-paths/

һ��������λ��һ�� m x n ��������Ͻ� ����ʼ������ͼ�б��Ϊ��Start�� ����

������ÿ��ֻ�����»��������ƶ�һ������������ͼ�ﵽ��������½ǣ�����ͼ�б��Ϊ��Finish������

���ܹ��ж�������ͬ��·����

![����](https://img-blog.csdnimg.cn/20190912160514978.png)

���磬��ͼ��һ��7 x 3 �������ж��ٿ��ܵ�·����

<b>˵��</b>��m �� n ��ֵ�������� 100��

<b>ʾ�� 1</b>:
```c
����: m = 3, n = 2
���: 3
����:
�����Ͻǿ�ʼ���ܹ��� 3 ��·�����Ե������½ǡ�
1. ���� -> ���� -> ����
2. ���� -> ���� -> ����
3. ���� -> ���� -> ����
```

<b>ʾ�� 2</b>:
```c
����: m = 7, n = 3
���: 28
```

<b>ʾ�� 3</b>:
```c
����: m = 23, n = 12
���: 193536720
```

<b>˼·��</b>���ö�̬�滮��

��̬�滮���01��

![��01](https://img-blog.csdnimg.cn/20190912160347481.png)

��̬�滮���02��

![��02](https://img-blog.csdnimg.cn/20190912160424714.png)

��̬�滮�������ӽṹΪ��`d[i,j] = d[i-1,j] + d[i,j-1]`

- ״̬��ͨ��
- 62 / 62 ��ͨ����������
- ִ����ʱ: 52 ms, ������ C# �ύ�л����� 93.18% ���û�
- �ڴ�����: 13.6 MB, ������ C# �ύ�л����� 17.65% ���û�

```c
public class Solution
{
    public int UniquePaths(int m, int n)
    {
        int[,] memo = new int[m, n];
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (i == 0)
                {
                    memo[i, j] = 1;
                }
                else if (j == 0)
                {
                    memo[i, j] = 1;
                }
                else
                {
                    memo[i, j] = memo[i - 1, j] + memo[i, j - 1];
                }
            }
        }
        return memo[m - 1, n - 1];
    }
}
```



