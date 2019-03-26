# Introduction

* 推箱子算法研究

var a = [1,2,3,4,1,2,3,6,7];

function quickSort(items, left, right) {

  var index;

  if (items.length > 1) {

​      index = partition(items, left, right);

​      console.log(index);

​      console.log(items)

​      if (left < index - 1) {

​          quickSort(items, left, index - 1);

​      }

​      if (index < right) {

​          quickSort(items, index, right);

​      }

  }

  return items;

}

function swap(items, firstIndex, secondIndex){

  var temp = items[firstIndex];

  items[firstIndex] = items[secondIndex];

  items[secondIndex] = temp;

}

function partition(items, left, right) {

  var pivot   = items[Math.floor((right + left) / 2)],

​      i       = left,

​      j       = right;

  while (i <= j) {

​      while (items[i] < pivot) {

​          i++;

​      }

​      while (items[j] > pivot) {

​          j--;

​      }

​      if (i <= j) {

​          swap(items, i, j);

​          i++;

​          j--;

​      }

  }

  return i;

}

console.log(quickSort(a, 0, a.length - 1));



http://www.ruanyifeng.com/blog/2011/04/quicksort_in_javascript.html