# [Gorm调试打印SQL](https://github.com/xpblog/say-something/issues/18)

[返回目录](https://github.com/xpblog/say-something)

### 单条打印
在操作前加DB加Debug()， 相当于将临时将日志级别改为Info
```go
DB.Debug().Where("id = ?", 6).First(&newData)

// [2023-05-17 10:50:10]  [5.09ms]  DELETE FROM `students`  WHERE (id = '6') 
```

### 全局打印
在DB配置文件中加Debug()
```go
func initDB() {
	url := "root:123456@tcp(127.0.0.1:3306)/student?&parseTime=True&loc=Local"
	db, err := gorm.Open("mysql", url)
	if err != nil {
		panic(err)
	}
	DB = db.Debug()
}
```
