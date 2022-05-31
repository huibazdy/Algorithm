## 二分查找专题

### 1. 二分查找

> 【**题702**】给定一个`n`个元素升序的整型数组`nums`和一个目标值`target`，写一个函数搜索`nums`中的`target`，如果目标值存在，则返回下标，否则返回`-1`。



```C++
/*V1.0：20220529 14:27 zhangdaoyuan*/
int search(vector<int>& nums,int target)
{
    int left = 0;
    int right = nums.size() - 1;
    int mid;
    
    while(left <= right)
    {
        mid = (right + left) / 2;
        if(target < nums[mid])
            right = mid - 1;
        else if(target > nums[mid])
            left = mid + 1;
        else
            return mid;
    }
    return -1;
}

/*V1.1：LeetCode官方题解*/
int search(vector<int>& nums,int target)
{
    int low = 0;
    int high = nums.size() - 1;
    while(low <= high)
    {
        int mid = (high - low) / 2 + low;
        int num = nums[mid];
        if(target = num)//应该把直接匹配的可能性放在前面？减少遍历次数？
        {
            return mid;
        }
        else if(target > num)
        {
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }
    return -1;
}
```



### 2. 猜数字大小

> 【**题374**】
> 猜数字游戏的规则如下：
>
> 每轮游戏，我都会从 1 到 n 随机选择一个数字。 请你猜选出的是哪个数字。
> 如果你猜错了，我会告诉你，你猜测的数字比我选出的数字是大了还是小了。
> 你可以通过调用一个预先定义好的接口 int guess(int num) 来获取猜测结果，返回值一共有 3 种可能的情况（-1，1 或 0）：
>
> -1：我选出的数字比你猜的数字小 pick < num
> 1：我选出的数字比你猜的数字大 pick > num
> 0：我选出的数字和你猜的数字一样。恭喜！你猜对了！pick == num
> 返回我选出的数字。
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode.cn/problems/guess-number-higher-or-lower
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



```C++
int guessNumber(int n) {
        int low = 1;
        int high = n;
        int mid;
        while(low <= high)
        {
            mid = (high - low) / 2 + low;
            if(guess(mid) == 0)
            {
                return mid; 
            }
            else if(guess(mid) == 1)
            {
                low = mid + 1;
            }
            else
            {
                high = mid - 1;
            }
        }
        return mid;
    }


//LeetCode官方解答
int guessNumber(int n) {
        int left = 1, right = n;
        while (left < right) { // 循环直至区间左右端点相同
            int mid = left + (right - left) / 2; // 防止计算时溢出
            if (guess(mid) <= 0) {
                right = mid; // 答案在区间 [left, mid] 中
            } else {
                left = mid + 1; // 答案在区间 [mid+1, right] 中
            }
        }
        // 此时有 left == right，区间缩为一个点，即为答案
        return left;
    }
```

