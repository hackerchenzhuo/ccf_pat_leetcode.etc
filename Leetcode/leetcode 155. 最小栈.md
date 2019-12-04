# 原创：leetcode 155. 最小栈

```c++
class MinStack {
public:
    /** initialize your data structure here. */
    //双栈。顺序天然相同
    
    stack<int> s;
    stack<int>min;
    MinStack() {
       
    }
    
    void push(int x) {
        
        if(min.empty()||x<=min.top()) min.push(x);
        s.push(x);
    }
    
    void pop() {
        if(s.top()==min.top()) min.pop();
        s.pop();
 
    }
    
    int top() {
        return s.top();
    }
    
    int getMin() {
        return min.top();
    }
};
 
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
 ``` 
