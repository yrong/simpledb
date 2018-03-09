# simpledb

this is a simple key-value db implementation

[Design Doc](https://github.com/yrong/bitcask/blob/master/doc/doc.md)


# Example

```
package main

import (
	"github.com/yrong/bitcask"
	"github.com/laohanlinux/go-logger/logger"
)

func main() {
	bc, err := bitcask.Open("exampleBitcaskDir", nil)
	if err != nil {
		logger.Fatal(err)
	}
	defer bc.Close()
	k1 := []byte("xiaoMing")
	v1 := []byte("毕业于新东方推土机学院")

	k2 := []byte("zhanSan")
	v2 := []byte("毕业于新东方厨师学院")

	bc.Put(k1, v1)
	bc.Put(k2, v2)

	v1, _ = bc.Get(k1)
	v2, _ = bc.Get(k2)
	logger.Info(string(k1), string(v1))
	logger.Info(string(k2), string(v2))
	// time.Sleep(time.Second * 10)
	// override
	v2 = []byte("毕业于新东方美容美发学院")
	bc.Put(k2, v2)
	v2, _ = bc.Get(k2)
	logger.Info(string(k2), string(v2))

}

```

`go run example/bitcask_main.go`

```
2016/01/16 16:56:11 bitcask_main.go:25 [info [xiaoMing 毕业于新东方推土机学院]]
2016/01/16 16:56:11 bitcask_main.go:26 [info [zhanSan 毕业于新东方厨师学院]]
2016/01/16 16:56:11 bitcask_main.go:32 [info [zhanSan 毕业于新东方美容美发学院]]
2016/01/16 16:56:11 bitcask_main.go:36 [info [毕业后的数据库：]]
2016/01/16 16:56:11 bitcask_main.go:41 [info [xiaoMing 已经毕业.]]
2016/01/16 16:56:11 bitcask_main.go:47 [info [zhanSan 已经毕业.]]
```

other Example: find it in `xxxx_test.go`

# TODO

- 优化数据结构，减少内存占用
- 增加merge功能
