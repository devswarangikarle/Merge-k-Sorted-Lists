# Merge-k-Sorted-Lists
You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.  Merge all the linked-lists into one sorted linked-list and return it.

class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        l = len(lists)
        if len(lists) == 0 or lists is None:
            return None
        
        def merge_2_linkedlist(l1, l2):
            dummy = ListNode()
            tail = dummy
            while l1 and l2:
                if l1.val > l2.val:
                    tail.next = l2
                    l2 = l2.next
                else:
                    tail.next = l1
                    l1 = l1.next
                tail = tail.next

            while l1:
                tail.next = l1
                l1 = l1.next
                tail = tail.next

            while l2:
                tail.next = l2
                l2 = l2.next
                tail = tail.next

            return dummy.next

        '''def sort(arr):
            if len(arr) > 1:
                left = arr[:(len(arr)//2)]
                right = arr[(len(arr)//2):]

                left_arr = sort(left)
                right_arr = sort(right)

                return merge_2_linkedlist(left_arr, right_arr)'''
                
        while len(lists) > 1:
            answer = []
            for i in range(0, len(lists), 2):
                left_arr = lists[i]
                if i+1 < len(lists):
                    right_arr = lists[i+1]
                else:
                    right_arr = None

                answer.append(merge_2_linkedlist(left_arr, right_arr))
            lists = answer
        return lists[0]
