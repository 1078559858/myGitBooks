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
        while(a[j] >= jizhun &&　i < j){
            j--;
        }

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
quickSort(array,0,array.length-1);//排完序后再看array是[2, 3, 4, 7, 8, 9, 12]
console.log(array)
```

