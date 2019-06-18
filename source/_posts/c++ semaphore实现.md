---
title: c++ semaphore实现
date: 2019-06-18 14:48:31
tags:
  - C++
  - 多线程
---

```C++
#include<iostream>
#include<thread>
#include<mutex>
#include<condition_variable>
using namespace std;

mutex mtx;

class semaphore{
private:
    int count;
    mutex mtx;
    condition_variable cv;
public:
    semaphore(int value = 1):count(value){}
    void wait(){
        unique_lock<mutex> lck(mtx);
        if(--count < 0){
            cv.wait(lck);
        }
    }
    void signal(){
        unique_lock<mutex> lck(mtx);
        if(++count<=0){
            cv.notify_one();
        }
    }
};

semaphore s1(0);
semaphore s2(0);
semaphore s3(0);

void func1(){
    cout<<"first"<<endl;
    s1.signal();
}
void func2(){
    s1.wait();
    cout<<"second"<<endl;
    s2.signal();
}
void func3(){
    s2.wait();
    cout<<"third"<<endl;
    s3.signal();
}
void func4(){
    s3.wait();
    cout<<"fourth"<<endl;
}


int main(){
    thread t1(func4);
    thread t2(func3);
    thread t3(func2);
    thread t4(func1);
    t1.join();  
    t2.join();
    t3.join();
    t4.join();
    return 0;
}
```