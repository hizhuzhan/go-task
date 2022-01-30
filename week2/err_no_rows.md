# 第二周作业

## 题目:  
```text
    我们在数据库操作的时候，
    比如 dao 层中当遇到一个 sql.ErrNoRows 的时候，
    是否应该 Wrap 这个 error，抛给上层。
    为什么，应该怎么做请写出代码？
```

## 解答
```go
//  当dao层遇到 sql.ErrNoRows 的时候，我认为不需要抛给上层；
//  因为这也算是查询出的一个结果。
//  我的示例代码如下：

package test

var name string
sql := "select name from users where id = ?"
param := 1
err := db.QueryRow(sql, param).Scan(&name)
if err != nil {
	if err == sql.ErrNoRows {
		// there were no rows, but otherwise no error occurred
	} else {
        errors.Wrap(500, thisMethodName + lineNo + sql + param)
	}
}

```