# interview-bit--math--city-tour

**-----> Question:**

There are A cities numbered from 1 to A. You have already visited M cities, the indices of which are given in an array B of M integers.

If a city with index i is visited, you can visit either the city with index i-1 (i >= 2) or the city with index i+1 (i < A) if they are not already visited.
Eg: if N = 5 and array M consists of [3, 4], then in the first level of moves, you can either visit 2 or 5.

You keep visiting cities in this fashion until all the cities are not visited.
Find the number of ways in which you can visit all the cities modulo 10^9+7.

Input Format

The 1st argument given is an integer A, i.e total number of cities.
The 2nd argument given is an integer array B, where B[i] denotes ith city you already visited.

Output Format

Return an Integer X % (1e9 + 7), number of ways in which you can visit all the cities.

Constraints

1 <= A <= 1000
1 <= M <= A
1 <= B[i] <= A

For Example 

Input:

A = 5
B = [2, 5]

Output:

6

Explanation:

All possible ways to visit remaining cities are :
1. 1 -> 3 -> 4
2. 1 -> 4 -> 3
3. 3 -> 1 -> 4
4. 3 -> 4 -> 1
5. 4 -> 1 -> 3
6. 4 -> 3 -> 1


**------> Code:**

#define ll long long
#define mod 1000000007

ll power(ll x,ll y){

    ll res=1; 
    while(y){
        if(y&1) res = (res*x)%mod; 
        y>>=1; 
        x = (x*x)%mod;
    }
    return res;
}

int Solution::solve(int A, vector<int> &B) {
    
    sort(B.begin(),B.end()); 
    vector<int>un_vis; 
    int i=1;
    un_vis.push_back(B[0]-1);
    for(;i<B.size();i++){
        un_vis.push_back(B[i]-B[i-1]-1);
    }
    un_vis.push_back(A-B[i-1]);
    int n = un_vis.size(); 
    ll fact[100000]={1}; 
    for(ll f=1;f<100000;f++) fact[f] = (f*fact[f-1])%mod;
    ll ans = 1,x=A-B.size(),p=1;
    for(i=0;i<n;i++){
        if(!un_vis[i]) continue;
        if(i!=0&&i!=n-1) ans = (ans*power(2,un_vis[i]-1))%mod;
        p = (p*fact[un_vis[i]])%mod;
    }
    ans = (ans*fact[x])%mod;
    ans = (ans*power(p,mod-2))%mod;
    return ans;
}

                      
 **# -------> important concept: Fermat's little theorem**
