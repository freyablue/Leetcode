#### 23. Merge k Sorted Lists(Hard)
You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.
````
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        k = len(lists)
        if k==0:
            return None            
        def merge(l1,l2):
            r = result = ListNode()
           
            while l1!=None and l2!=None:
                if l1.val < l2.val:
                    result.next = ListNode(l1.val,None)
                    l1 = l1.next
                else:
                    result.next = ListNode(l2.val,None)
                    l2 = l2.next
                result = result.next
            result.next = l1 or l2
            return r.next
        def merge_multiple(start, end, lists):
            if start==end:
                return lists[start]
            if end-start==1:
                return merge(lists[start],lists[end])
            if start<end:
                mid = (start+end)//2
                left_merge =  merge_multiple(start,mid,lists)
                right_merge = merge_multiple(mid+1,end,lists)
                return merge(left_merge,right_merge)
        
        return merge_multiple(0,k-1,lists)
                
````

Merge all the linked-lists into one sorted linked-list and return it.
#### 79. Word Search(Medium)
