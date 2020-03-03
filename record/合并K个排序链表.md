# [23. 合并K个排序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)
### 题意
合并k个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。
### 思路
用最小堆
### 代码
```cgo
class Heap{
public:
       static const int start =1;
    vector<ListNode*> h;
    int index;
    Heap(int n) {
        index=start;
        h=vector<ListNode*>(n+1,NULL);
    }
    void Swap(int a, int b) {
        ListNode* tamp = h[b];
        h[b] = h[a];
        h[a] = tamp;
    }
    bool Empty() {
        if(index == start) return true;
        return false;
    }
    void Print() {
        for(int i=start; i<index; i++) cout<<h[i]->val;
        cout<<endl;
    }
    void Insert(ListNode* a) {
        if(a == NULL) return;
        h[index++] = a;
        int p=index-1;
        while(p/2>0) {
            if(h[p]->val < h[p/2]->val) Swap(p, p/2);
            p/=2;
        }
    }
    ListNode* Delete() {
        if(index==start) return NULL;
        ListNode* res=h[start];
        h[start] = h[--index];
        int p=start;
        while(p < index) {
            int left=p*2, right=p*2+1, nextP=p;
            if(left<index && h[left]->val < h[nextP]->val) nextP=left;
            if(right<index && h[right]->val < h[nextP]->val) nextP=right;
            if(nextP==p) break;
            Swap(nextP, p);
            p=nextP;
        }
        return res;
    }
};
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.size() == 0) return NULL;
        ListNode *p=NULL,*head=NULL;
        Heap *heap= new Heap(lists.size());
        for(int i=0; i<lists.size(); i++){
            heap->Insert(lists[i]);
        }
        int k=0;
        while(!heap->Empty()) {
            ListNode* tamp = heap->Delete();
            if(p==NULL) {
                p=tamp;
                head=p;
            }else {
                p->next= tamp;
                p=p->next;
            }
            if(tamp->next != NULL) heap->Insert(tamp->next);
        }
        if(p!=NULL) p->next =NULL;
        return head;
    }
};
```