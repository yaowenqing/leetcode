Given a collection of distinct integers, return all possible permutations.

>Example:
Input: [1,2,3]
Output:
[
[1,2,3],
[1,3,2],
[2,1,3],
[2,3,1],
[3,1,2],
[3,2,1]
]

思路：用递归的思路实现。
从第一个数所在的位置开始，完成从第二个数到最后一个数的全排列，然后依次将所有的数与第一个数交换，再完成第二个数到最后一个数的全排列，为了不破坏数组的有序性，每次完成全排列之后再交换回来。

以[1,2,3,4]为例。

首先会交换start(此时为0)和i(此时为0)，注意每次循环的第一步相当于没有交换，然后完成对于[2,3,4]的全排列（递归实现），之后再交换回来。

然后交换start(此时为0)和i(此时为1)，数组为[2,1,3,4]，完成对于[1,3,4]的全排列，之后再交换回来，变回[1,2,3,4]。

然后再交换start(此时为0)和i(此时为2)，数组为[3,2,1,4]，依次类推。

### 代码

```
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    public List<List<Integer>> permute(int[] nums) {
        perm(nums,0,nums.length-1);
        return res;
    }
    
    public void perm(int[] nums,int start,int end){
        if(start==end){//全排列遍历到了末尾
            List<Integer> list =new ArrayList<>();
            for(int i=0;i<nums.length;i++){
                list.add(nums[i]);//直接把每个元素依次放入数组并加入全排列列表中
            }
            res.add(list);
        }else{
            for(int i=start;i<=end;i++){
                swap(nums,start,i);
                perm(nums,start+1,end);//完成对第二个数字到最后一个数字的全排列
                swap(nums,i,start);//不破坏数组的原始顺序，再交换回来
            }
        }
    }

```
