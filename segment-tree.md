# Segment tree

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
