# Segment tree

```C++
vector<long> tree;

 int first_power_of_2(int n) {
     if ((n&(n-1)) != 0) { // n is not power of 2
         int shift = 0;
         while (n) {  
             n >>= 1;  
             shift ++;
         }  
         n = 1<<shift;
     }
     return n;
 }

 void build(vector<int> &nums) {
     int n = nums.size();
     if (n == 0)
         return;

     n = first_power_of_2(n);

     tree = vector<long>(n*2, 0);
     for (int i = 0; i < nums.size(); i++) {
         tree[i+n] = nums[i];
     }
     for (int i = n-1; i > 0; i--) {
         tree[i] = tree[2*i] + tree[2*i+1];
     }
 }

 void update(int i, int val) {
     int n = tree.size()/2;
     i += n;
     tree[i] = val;

     while (i > 0) {
         int l = i%2 == 0 ? i : i-1;
         int r = l+1;
         i = l/2; 
         tree[i] = tree[l] + tree[r];
     }
 }

 int sumRange(int i, int j) {
     int n = tree.size()/2;
     int l = i+n, r = j+n;
     int ans = 0;

     while (l <= r) {
         if (l%2 != 0) {
             ans += tree[l++];
         }
         if (r%2 == 0) {
             ans += tree[r--];   
         }
         l = l/2;
         r = r/2;
     }
     return ans;
 }
```
