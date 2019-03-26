# 快排

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

参考：https://www.cnblogs.com/venoral/p/5180439.html
```

