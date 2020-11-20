# Monotonic stack

<p>Monotonic stack is a special stack, always maintaining its elements monotonic/ordered. An element can only be pushed into stack only when:<br>

- stack is empty<br />
- stack's top element keeps a monotonic order with comming new element



So the stack needs to pop out element until it meets the requirement before pushing new element.


What problem does monotonic stack solve ? <br/>
For an array data[], let's say for any given index i, try to get the first element smaller than data[i] when searching from i to left or right. 
Monotonic stack is used to solve this problem in a O(n) time.

```C++
// index:  0  1  2  3  4  5
// data : [2, 1, 5, 6, 2, 3]. 
vector<int> data({2,1,5,6,2,3});
stack<int> st;

vector<int> left(data.size(), -1);
vector<int> right(data.size(), -1);

for (int i = 0; i < data.size(); i++) {
    if (st.empty() || data[st.top()] <= data[i]) {
        /* search from i to left, the first element smaller than data[i] is data[st.top()] */
        left[i] = st.empty() ? -1 : st.top();
        st.push(i);
    } else {
        int j = st.top();
        /* search from j to right, the first element smaller than data[j] is data[i] */
        right[j] = i;
        st.pop();
        i--;
    }
}
// Results:
// index:   0   1   2   3   4   5
// data :  [2,  1,  5,  6,  2,  3]
// left : [-1, -1,  1,  2,  1,  4] 
// right: [ 1, -1,  4,  4, -1, -1] 
```


Related Leetcode problems:<br/>
[Leetcode 84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)<br/>
[Leetcode 85. Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/)<br/>
[Leetcode 316. Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters/)<br/> 
[Leetcode 496. Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/) <br/>
[Leetcode 503. Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/]) <br/>
[Leetcode 739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) <br />
[Leetcode 901. Online Stock Span](https://https://leetcode.com/problems/online-stock-span/) <br />






