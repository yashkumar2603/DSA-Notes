**Copy List with random pointer**
https://leetcode.com/problems/copy-list-with-random-pointer/description/

```C++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        unordered_map<Node*, Node*> mp;
        mp[NULL] = NULL;
        
        Node* cur = head;
        while(cur)
        {
            Node* copy = new Node(cur->val);
            mp[cur] = copy;
            cur = cur->next;
        }

        cur=head;
        while(cur)
        {
            Node* copy = mp[cur];
            copy->next = mp[cur->next];
            copy->random = mp[cur->random];
            cur=cur->next;
        }
        return mp[head];
    }
};

```

**Add two numbers(the carray makes it difficult) -** 
https://leetcode.com/problems/add-two-numbers/description/

```C++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode();
        ListNode* cur = dummy;
        int carry = 0;
        while (l1 != nullptr || l2 != nullptr || carry != 0) {
            int v1 = (l1 != nullptr) ? l1->val : 0;
            int v2 = (l2 != nullptr) ? l2->val : 0;
            int val = v1 + v2 + carry;
            
            carry = val / 10;
            val = val % 10;
            cur->next = new ListNode(val);
            cur = cur->next;
            
            l1 = (l1 != nullptr) ? l1->next : nullptr;
            l2 = (l2 != nullptr) ? l2->next : nullptr;
        }
        return dummy->next;
    }
};
```

**Find Duplicate Integer (question on slow and fast pointers)**
https://leetcode.com/problems/find-the-duplicate-number/description/

The algorithm is that we make the linked list by making the nums(i] point to i for every element, that way, 2 or more nodes will be pointing at the same place.
We detect the cycle then, using Floyd's Algorithm 
<font color="#e36c09">Memorize this question, no other choice fr</font>
```C++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = 0, fast = 0;
        while (true) {
            slow = nums[slow];
            fast = nums[nums[fast]];
            if (slow == fast) {
                break;
            }
        }
        int slow2 = 0;
        while (true) {
            slow = nums[slow];
            slow2 = nums[slow2];
            if (slow == slow2) {
                return slow;
            }
        }
    }
};
```

Reverse in K-groups - 
https://leetcode.com/problems/reverse-nodes-in-k-group/

```C++
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        int s =0;
        ListNode* curr = head;
        while(curr!=NULL)
        {
            s++;
            if(s>=k)
        {
            break;
        }
        curr = curr->next;
        }
        
        if(s<k)
        {
            return head;
        }
        ListNode* h = head;
        curr = head;
        for(int i =0;i<k-1;i++)
        {
            curr = curr->next;
        }
        ListNode* nh = curr->next;
        curr->next = NULL;
        ListNode* p =NULL;
        ListNode* c =h;
        ListNode* n = NULL;
        while(c!=NULL)
        {
            n = c->next;
            c->next = p;
            p = c;
            c=n;
        }
        h->next = reverseKGroup(nh,k);
        return curr;  
    }
};
```

**Merge K-sorted Lists -** 
https://leetcode.com/problems/merge-k-sorted-lists/description/
```C++
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<pair<int, ListNode*>, vector<pair<int, ListNode*>>, greater<pair<int, ListNode*>>> pq;

        for(int i = 0; i < lists.size(); i++) {
            if (lists[i] != nullptr) {
                pq.push({lists[i]->val, lists[i]});
            }
        }
        ListNode* dummy = new ListNode(-1, NULL);
        ListNode* temp = dummy;
        while(!pq.empty())
        {
            auto curr = pq.top();
            pq.pop();
            temp->next = curr.second;
            temp = temp->next;
            if(curr.second->next) pq.push({curr.second->next->val, curr.second->next});
        }

        return dummy->next;
    }
};
```

**Rotate List right -** 
https://leetcode.com/problems/rotate-list/
```C++
ListNode* rotateRight(ListNode* head, int k) {
        if (!head || !head->next || k == 0) return head;
        // Compute the length of the linked list
        int n = 1;
        ListNode* temp = head;
        while (temp->next) {
            temp = temp->next;
            n++;
        }
        // If k is a multiple of n, no rotation is needed
        k = k % n;
        if (k == 0) return head;
        // Find the new head and the new tail
        int c = n - k;
        ListNode* dummy = head;
        while (c > 1) {
            dummy = dummy->next;
            c--;
        }
        // Set the new head and the new tail
        ListNode* newHead = dummy->next;
        dummy->next = NULL;
        temp->next = head;
        return newHead;
    }
```

**Find middle of the linked List using slow and fast pointers, in O(n/2) -** 
```C++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* fast = head;
        ListNode* slow = head;
        if(head==NULL) return NULL;
        while(fast!=NULL && fast->next!=NULL)
        {
            slow=slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
};
```

detect cycle, Floyd's algo - 
Explanation:
1. **Cycle Detection**: Use two pointers, `slow` and `fast`. Move `slow` one step at a time and `fast` two steps at a time. If there is a cycle, `slow` and `fast` will eventually meet inside the cycle.
2. **Finding Cycle Start**: Once a cycle is detected, use another pointer `entry` starting from the head and move both `entry` and `slow` one step at a time. The point where they meet is the start of the cycle.
This approach ensures an efficient O(n) time complexity and O(1) space complexity, making it optimal for detecting cycles in a linked list.
```C++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if (!head || !head->next) return NULL;
        ListNode* slow = head;
        ListNode* fast = head;

        // Detect if there is a cycle
        while (fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                // Cycle detected
                ListNode* entry = head;
                while (entry != slow) {
                    entry = entry->next;
                    slow = slow->next;
                }
                return entry; // Entry point of the cycle
            }
        }
        return NULL; // No cycle
    }
};
```

delete middle node of linked list - 
https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/
```C++
class Solution {
public:
    int length(ListNode* head){
        ListNode* temp = head;
        int count = 0;
        while(temp!=NULL){
            count++;
            temp=temp->next;
        }
        return count;
    }
    ListNode* deleteMiddle(ListNode* head) {
        if(head==NULL || head->next==NULL) return NULL;
        int n = length(head);
        int t = n/2;
        ListNode* temp = head;
        for(int i=0;i<t;i++){
            if(i==t-1){
                ListNode* todelete = temp->next;
                temp->next=temp->next->next;
                delete todelete;
            }
            temp=temp->next;
        }
        return head;
    }
};
```

Segregate odd and even indexed nodes - 
https://leetcode.com/problems/odd-even-linked-list/
```C++
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if (head == nullptr || head->next == nullptr)
            return head; // If the list is empty or has only one node, return as is
        ListNode* odd = head; // Initialize odd pointer to the head of the list
        ListNode* even = head->next; // Initialize even pointer to the second node
        ListNode* temp = even; // Store the start of the even list
        while (even != nullptr && even->next != nullptr) {
            // Update odd and even pointers to skip one node each
            odd->next = odd->next->next;
            even->next = even->next->next;
            odd = odd->next;
            even = even->next;
        }
        // Connect the end of the odd list to the start of the even list
        odd->next = temp;
        return head; // Return the modified list
    }
};
```

