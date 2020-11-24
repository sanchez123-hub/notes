### 通过结构体生成JSON

```go
//成员变量名首字母大写
type IT struct{
    Company   string
    Subjects  []string
    IsOk       bool
    Price     float64
}

//定义结构体变量
s := IT{"itcast",[]string{"go","c++"."python"},true,66.6}

//编码，生成json文本
//格式化编码：json.MarshalIndent(s,"","	")
buf,err := json.Marshal(s)
if err != nil{
    fmt.Println("err = ",err)
    return
}
fmt.Println("buf = ",string(buf))
```

对结构体二次编码

```go
type IT struct{
    Company   string    `json:"-"`  //此字段不会输出在屏幕上
    Subjects  []string   `json:"subjects"`
    IsOk       bool		`json:",string"`//以字符串输出
    Price     float64
}
```

### 通过map生成JSON

```go
m := make(map[string]interface{},4)
m["company"] = "itcast"
m["subjects"] = []string{"go",c++}
m["isok"] = true
m["price"] = 66.6

result, err := json.Marshal(m)
```

### JSON解析到结构体

```go
type IT struct{
    Company   string    `json:"company"`
    Subjects  []string   `json:"subjects"`
    IsOk       bool		`json:"isok"`
    Price     float64	 `json:"price"`
}

func main(){
    jsonBuf := `
    {"company":"itcast","subjects":["go","c++","python"],"isok":true,"Price":66.6}
    `
    //定义结构体
	var temp IT
    err := json.Unmarshal([]byte(jsonBuf),&temp)//引用传递
    if err != nil{
        return
    }
    fmt.Println(temp)
    fmt.Printf("temp = %+v\n",temp)
}
```

##### json解析到map时无法获取到变量值字符串的解决方法

```go
//m为解析目标map
for key,value := range m{
    switch data := value.(type) {
        case string:
        str = data
        fmt.Printf(str)
        case []interface{}://subjects的类型
    }
}
```



