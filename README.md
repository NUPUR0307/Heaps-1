# Heaps-1

## Problem1 
TC: O(nlogk)
SC: O(k)

//Approach:
1. We will use priority queue to store the elements of the array 
2. if the size of priority queue is more than k then we will poll the elements
3. We will return the peek element as we are using min heap and at the end we will be left with the kth largest element in the pq

Kth largest in Array (https://leetcode.com/problems/kth-largest-element-in-an-array/)

class Solution {
    public int findKthLargest(int[] nums, int k) {
        if(nums == null || nums.length == 0){
            return -1;
        }

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        for(int num : nums){
            pq.offer(num);

            if(pq.size() > k){
                pq.poll();
            }
        }

        return pq.peek();
    }
}

## Problem2
TC: O(n log k)
SC: O(n)

//Approach:
1. We will use a priority queue to store the first node of all the lists 
2. we will form a new Linked List and add the next node to the priority queue

Merge k Sorted Lists(https://leetcode.com/problems/merge-k-sorted-lists/)

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null || lists.length == 0){
            return null;
        }

        PriorityQueue<ListNode> pq = new PriorityQueue<>((ListNode a, ListNode b) -> a.val - b.val);

        for(ListNode node : lists){
            if(node != null){
                pq.offer(node);
            }
        }

        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;

        while(!pq.isEmpty()){
            ListNode min = pq.poll();
            curr.next = min;
            curr = curr.next;

            if(min.next != null){
                pq.offer(min.next);
            }
        }

        return dummy.next;

    }
}