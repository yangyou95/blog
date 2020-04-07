# Interface 和 Virtual Function

## Virtual Function

在一个base class里, 我们可以定义virtual function如下:

```c++
class parent{
  public:
  	virtual void func(/* args */){
        /* codes */
  	}
};
```

我们在子类里, 可以override这个function如下:

```c++
class child: pubic parent{
    public:
    void func(/* args */) override {
        /* codes */
    }
};
```

在这种情况下, 子类也可以不对func做修改重写.

## Interface 

如过我们想强制子类必须要重写某个func, 我们需要在基类里的virtual func为一个**Pure Virtual function**. Pure virtual function强制要求在子类里重新定义该函数, 因此, 我们无法初始化一个基类的对象, 若想要初始化, 需要先在子类里重写该函数, 之后初始化时直接初始化子类的对象.

```c++
class parent{
  public:
  	virtual void func(/* args */) = 0; // 定义一个pure virtual function
};

class child: pubic parent{
    public:
    void func(/* args */) override { // implment the pure virtual function
        /* codes */
    }
};
```

