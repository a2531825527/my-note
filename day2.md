## 209.长度最小的子数组
  - **题目：给定一个含有 n 个正整数的数组和一个正整数 s ，找出该数组中满足其和 ≥ s 的长度最小的 连续 子数组，并返回其长度。如果不存在符合条件的子数组，返回 0。**
    1. ### 暴力解法
        - #### 两个for循环，然后不断的寻找符合条件的子序列，时间复杂度很明显是O(n^2)。
            ```csharp
            public int MinSubArrayLen(int target, int[] nums)
            {
                int end=0;
                int l;
                int r;
                int sl=0;
                for ( l=0;l<nums.Length ;l++) 
                {
                    int s = 0;
                    for (r=l;r<nums.Length ;r++) 
                    {
                        s += nums[r];
                        if (s >= target) 
                        {
                            sl = r - l + 1;
                            if (end==0) 
                            {
                                end = sl;
                            }
                            else if (sl<end) 
                            {
                                end=sl;
                            }
                            break;
                        }
                    }
                }
                return sl;
            }
            ```
    2. ### 滑动窗口
        - #### 所谓滑动窗口，就是不断的调节子序列的起始位置和终止位置，从而得出我们要想的结果。
            
            **窗口就是 满足其和 ≥ s 的长度最小的 连续 子数组。**
            
            **窗口的起始位置如何移动：如果当前窗口的值大于等于s了，窗口就要向前移动了（也就是该缩小了）。**
            ```csharp
            public int MinSubArrayLen1(int target, int[] nums) 
            {
                int end=0;
                int i=0;
                int j;
                int s = 0;
                int sl;
                for (j=0;j<nums.Length ;j++) 
                {
                    s += nums[j];
                    while (s >= target) 
                    //不要以为for里放一个while就以为是O(n^2).
                    //主要是看每一个元素被操作的次数，每个元素在滑动窗后进来操作一次，出去操作一次.
                    //每个元素都是被操作两次，所以时间复杂度是 2 × n 也就是O(n)。
                    {
                        sl = j - i+1;
                        if (end == 0)
                        {
                            end = sl;
                        }
                        else if (sl < end)
                        {
                            end = sl;
                        }

                        s -= nums[i];
                        i++;
                    }
                    
                }
                return end;
            }
            ```
## 59.螺旋矩阵II
- **题目：给定一个正整数 n，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。**
    1. ### 本题并不涉及到什么算法，就是模拟过程
        ```csharp
        public int[][] GenerateMatrix(int n)
        {
            int m=n*n;
            int[][] ints = new int[n][];
            for (int ii = 0; ii < n; ii++)
                ints[ii] = new int[n];
            int result=1;
            int i;
            int j;
            int a=0;int b=n-1;
            while (result<m) 
            {
                i = a;  
                for (j=a; j < b; j++)
                {
                    ints[i][ j] = result;
                    result++;
                }
                for (i=a; i < b; i++)
                {
                    ints[i][j] = result;
                    result++;
                }
                for (j=b; j > a; j--)
                {
                    ints[i][j] = result;
                    result++;
                }
                for (i=b; i > a; i--)
                {
                    ints[i][j] = result;
                    result++;
                }
                a++; b--;
            }
            if (n%2!=0) { ints[n / 2 ][n / 2 ]=m; }
            //NOTE:注意奇数时，中间的数要单独赋值.
            return ints;
        }
        ```

