## 704. 二分查找 
- **题目：给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。**
- ### 二分法的重点在于确定搜索的区间，依据区间来界定边界的判断。
    1. #### 区间为左闭右闭
        - 左闭右闭的区间划分意味着目标值可能与边界值相等，即while (left <= right) 的判断中，边界重合是有意义的。
            ```csharp
            public int Search(int[] nums, int target)
            {
                int L = 0;
                int R = nums.Length-1;
                int m ;
                while (L<=R) 
                { 
                    m = (R - L) / 2 + L;
                    //由于是闭区间，当目标值不在区间内时，要改变区间的边界
                    if (target < nums[m])
                    {
                        R = m-1;
                    }
                    else if (target > nums[m])
                    {
                        L = m+1;
                    }
                    else
                    {
                        return m;
                    }
                }
                return -1;
            }
            ```


## 27. 移除元素 
- **题目:给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。**

    **不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并原地修改输入数组。**

    **元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。**
- ### 由于数组中的元素不能删除只能覆盖，所以每次移除元素都需要将后一位的元素往前移动。
  1. #### 暴力解法 
       - 双重for循环暴力解法，每遇到一个需要移除的元素，便进入内循环依次将该元素后面的元素往前覆盖。
            ```csharp
            public int RemoveElement(int[] nums, int val)
            {

              int length = nums.Length;
              for (int i = 0; i < length; i++)
              {
                  if (nums[i] == val)
                  {
                      for (int j = i + 1; j < length; j++)//如果需要移除的元素是最后一位就不需要移动了
                      {
                          nums[j - 1] = nums[j];
                      }
                      length--;
                      i--;// 因为下标i以后的数值都向前移动了一位,不知道后一位是否也需要移除，所以i也向前移动一位,
                  }
              }
            return length;
            }
            ```
  2. #### 双指针法
       - **双指针法（快慢指针法）： 通过一个快指针和慢指针在一个for循环下完成两个for循环的工作。**

            **快指针：寻找新数组的元素 ，新数组就是不含有目标元素的数组**
            
            **慢指针：指向更新 新数组下标的位置**
            ```csharp
            public int RemoveElement1(int[] nums, int val) 
            {
                int j=0;
                for (int i=0;i<nums.Length ;i++) 
                {
                    if (nums[i] != val) 
                    //快指针指向非目标值元素时，将该值赋值给慢指针索引的元素。指向目标值时，快指针跳过该元素，检查下一个元素。
                    {
                        nums[j++]= nums[i]; //j++先取j的值，然后再自增。
                    }
                }
                return j + 1;
            }
            ```