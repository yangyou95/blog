# 指针和引用

# 引用可以理解为一个变量的别名

例如, 这段代码中, b就是a变量的一个别, 更改b的值, a也会更改

```c++
int main(){
	int a = 10;
	int& b = a;
	b = 20;
	cout << "a = "<< a <<endl;
	cout << "b = "<< b <<endl;
}
```

输出

```
a = 20
b = 20
```

## 引用Swap举例

```c++
void swap(int &a, int &b){
    int temp = 0;
    temp = a;
    a = b;
    b = temp;
}

int main(){
    int a = 10;
    int b = 20;
    swap(a, b);
    cout << "a = "<<a<<endl;
    cout << "b = "<<b<<endl;
}
```

## 指针Swap

```c++
void swap(int* a, int* b){
    int* temp = NULL;
    temp = a;
    a = b;
    b = temp;
}

int main(){
    int a = 10;
    int b = 20;
    swap(a, b);
    cout << "a = "<<a<<endl;
    cout << "b = "<<b<<endl;
}
```

