### 改动说明

1. 在 ThreadPool.h 和 example.cpp 中增加了中文注释。
2. 把少数一些嵌套的变量提取出来了，方便调试。如：

把
```c++
auto task = std::make_shared< std::packaged_task<return_type()> >(
        std::bind(std::forward<F>(f), std::forward<Args>(args)...)
    );
```
改成了
```c++
auto callableBind = std::bind(std::forward<F>(f), std::forward<Args>(args)...);
auto task = std::make_shared< std::packaged_task<return_type()> >(callableBind);
```
3. 通过clang-format格式化了代码。
4. 给条件判断后的单行语句增加了括号。如：

把
```c++
for (auto &&result: results)
  std::cout << result.get() << ' ';
```
改成了
```c++
for (auto &&result: results) {
  std::cout << result.get() << ' ';
}
```
5. example.cpp 中增加耗时统计。


---

ThreadPool
==========

A simple C++11 Thread Pool implementation.

Basic usage:
```c++
// create thread pool with 4 worker threads
ThreadPool pool(4);

// enqueue and store future
auto result = pool.enqueue([](int answer) { return answer; }, 42);

// get result from future
std::cout << result.get() << std::endl;

```
