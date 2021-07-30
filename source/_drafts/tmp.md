### centos clear old kernels
1. `rpm -q kernel`   
    list current all kernels

2. `sudo yum install yum-utils`    
    `sudo package-cleanup --oldkernels --count=2`


### virtualbox virtual disk
#### disk compact
1. prerequisite: handle zero block
- linux vm
```
sudo dd if=/dev/zero of=/bigemptyfile bs=4096k
sudo rm -rf /bigemptyfile
```

- window vm
```
// download and install SDelete tool
sdelete -s

```

2. compact
`VBoxManage modifyhd vm.vdi --compact`

#### disk resize(default size:M)
`VBoxManage modifymedium Debian.vdi --resize 30960 --compact` 


### thread-safe initialization of data

### thread-safe singleton
1. using call_once & once_flag
```cpp
class  Singleton {
private:
  Singleton() = default;
  ~Singleton() = default;
  Singleton(Singleton const& ) = delete;
  Singleton(Singleton &&) = delete;

  static Singleton* instance;
  static std::once_flag only_once;

public:
  static Singleton* get_instance() {
    std::call_once(only_once, Singleton::initSingleton);
    return instance;
  }

  static void initSingleton() {
    instance = new Singleton();
  }

};

Singleton* Singleton::instance = nullptr;
std::once_flag Singleton::only_once;

```

2. static variable with block scope
```cpp
class Singleton {
private:
  Singleton() = default;
  ~Singleton() = default;
  Singleton(Singleton const&) = delete;
  Singleton(Singleton&&) = delete;

public:
  static Singleton& get_instance() {
    static Singleton instance;
    return instance;
  }

};
```

### basic recusive template
```cpp

template <typename T, size_t SIZE , size_t N>
struct make_array_n {
    using type = typename make_array_n<std::array<T, SIZE>, SIZE, N - 1>::type;
};

template <typename T, size_t SIZE>
struct make_array_n<T, SIZE, 1> {
    using type = std::array<T, SIZE>;
};

template <typename T, size_t SIZE, size_t N>
using make_array_n_t = typename make_array_n<T, SIZE, N>::type;

```


### c++ initialization
![c++ initialization](/images/cpp_init.jpg)

