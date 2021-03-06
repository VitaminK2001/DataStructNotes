# 堆排序

[堆排序(heapsort)_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Eb41147dK?from=search&seid=5592152238569145386&spm_id_from=333.337.0.0)

一共分为三个部分

---

第一个部分 保证堆内有序

无论大根堆 小根堆 每一个小堆肯定是有序的（根节点最大 最小）

而要保证这一点需要用到递归

---

递归的过程

从根节点开始，一次比较根节点和两个子节点的大小关系，

以大根堆为例，有两种情况

- 根结点最大
不用移动
- 子节点有比根节点大的
移动（真正的）根节点和该子节点

之后在移动的子节点的位置重复上述过程

递归的终止条件是发现该节点的位置超过数组的长度

---

---

第二个部分 构建堆

首先需要构建出一个堆才能实行堆内有序的操作

构建堆的方法和完全二叉树的性质有关

如果完全二叉树的结点个数为n

从0开始给节点编号即从0~n-1号

则第 i 号结点的parent结点是 (i-1)/2（向下取整）

第 i 号结点的子节点是 2*i+1 和 2*i+2

从最后一个堆的parent节点开始施行上述堆内排序的算法

每次结点的序号-1 直到最终达到根节点

---

---

第三个部分 交换堆首堆尾

以大根堆为例 堆首是最大的元素，和堆尾的元素交换位置以后就完成了最大的元素的排序

接下来只需要对 n-1 个元素排序即可，即重新进行堆内排序，这个堆值的是整体，所以从根节点开始

因为已经不需要对堆尾的最大元素排序了，所以堆的大小变成n-1

---

代码部分

```java
package 排序.堆排序;

public class HeapSort {
    public static void main(String[] args) {
        int [] tree = {1, 3, 4, 5, 2, 7, 9, 20, 39, 26, 66, 48, 77};
        HeapSort s = new HeapSort();
        s.heapSort(tree, 13);
        for(int num : tree){
            System.out.println(num);
        }
    }
    public void heapify(int[] tree, int n, int i){
        if(i >= n) return;
        int c1 = 2*i+1;
        int c2 = 2*i+2;
        int max = i;
        if(c1 < n && tree[c1] > tree[max]){
            max = c1;
        }
        if(c2 < n && tree[c2] > tree[max]){
            max = c2;
        }
        if(max != i){
            swap(tree, max, i);
            heapify(tree, n, max);
        }
    }

    private void swap(int[] tree, int max, int i) {
        int temp = tree[max];
        tree[max] = tree[i];
        tree[i] = temp;
    }

    public void build_heap(int[] tree, int n){
        int last_node = n-1;
        int parent = (last_node-1)/2;
        int i;
        for(i = parent; i >= 0; --i){
            heapify(tree, n, i);
        }
    }
    public void heapSort(int [] tree, int n){
        build_heap(tree, n);
        int i;
        for (i = n-1; i >= 0; --i){
            swap(tree, i, 0);
            heapify(tree, i, 0);
        }
    }
}
```
