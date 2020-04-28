# 多线程

##　参考资料

<https://liam.page/2017/05/16/first-step-on-multithread-programming-of-cxx/>

<https://www.youtube.com/user/matsbror/videos>

## 注意事项

* Thread variables that go out of scope kills the thread
* Make sure variables accessed in a thread may not be out of scope

### 相关函数

* std::thread::hardware_concurrency() : 显示可用核心数
* std::thread::id a_thread_id: Type to hold a thread id
* std::this_thread::get_id() : return executing threads id
* thr.get_id() : return id of a thread thr
* Thread id vairables can be compared and ordered

## Data Racing

以下面代码为例

```c++
void function_1() {
    for (int i = 0; i>-100;i--){
        cout << "From t1: " << i << endl;
    }
        
}

int main() {
    std::thread t1(function_1);

    for (int i = 0; i<100; i ++)
        cout <<"From main: "<<i <<endl;

    t1.join();
    return 0;
}
```

在运行中, 我们会发现有这样混乱的结果:

```
From t1: -35
From t1: -36
From t1: -37
From t1: -38
From t1: -39
From t1: -40
From t1: -41
From t1: -42
From t1: -43
From t1: -44
From t1: -45
From t1: -46
From t1: -47
From main: From t1: -48
From t1: -49
From t1: 91-50
From main: 92

From t1: -51
From t1: -52
From t1: -53
From main: From t1: -54
93From t1: -55

From main: 94
From main: 95
From main: 96
From t1: From main: 97
-56From main: 98
```

这种混乱的结果是, 因为程序运行时, 两个线程(main thread 和 t1) 都在争抢资源 cout.

### Mutex

Mutex可以用来解决这种相同资源被多个线程争抢的现象, mutex的核心是通过Lock把要保护的资源锁住, 在操作执行过后再解锁, 在被锁住期间, 其他线程不能使用该资源. 上面的代码加入mutex后如下:

```
std:: mutex mu;

void shared_print(string msg, int id){
    mu.lock();
    cout << msg << id <<endl;
    mu.unlock();
}

void function_1() {
    for (int i = 0; i>-100;i--){
        shared_print(string("From t1: "), i);
    }
        
}

int main() {
    std::thread t1(function_1);

    for (int i = 0; i<100; i ++)
        shared_print(string("From main: "), i);

    t1.join();
    return 0;
}
```

