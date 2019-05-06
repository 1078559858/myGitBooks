# 快排

## 原理

找一个基准数,数据循环,把小于基准数放左边,大于基准数放右边. 然后分别对基准数左边和右边的数据进行循环操作,直到没有数据可以转换.

## 时间复杂度

最优: 每次基准数左右两边的数据都是相同的, 那么时间复杂度是O(logn)

最差: 每次基准数都是最小或者最大的数,那么时间复杂度是(On^2)

平均: O(nlogn)

## 实现1

[参考](https://www.cnblogs.com/venoral/p/5180439.html)

## 实现2

[参考](http://www.ruanyifeng.com/blog/2011/04/quicksort_in_javascript.html)

## 以最左边为基准

```javascript
function quickSort (a, left, right){
    if(left >= right){
        return;
    }

    var jizhun = a[left];
    var i = left;
    var j = right;

    while(i !== j){
        //必须要有等号
        //必须要从右开始检查
        while(a[j] >= jizhun &&　i < j){
            j--;
        }

        //必须要有等号
        while(a[i] <= jizhun && i < j){
            i++;
        }

        if(i < j ){
            var t = a[i];
            a[i] = a[j]
            a[j]  = t;
        }
    }

    a[left] = a[i]
    a[i] = jizhun;

    quickSort(a, left, i - 1);
    quickSort(a, i +1, right);
}

var array=[4,7,2,8,3,9,12];
quickSort(array,0,array.length-1);
console.log(array)


```

