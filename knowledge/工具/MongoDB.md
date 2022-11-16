# MongoDB

## 创建数据库和用户

1. 添加数据库: `use 数据库名`
2. 此时数据库有了，但是默认不会显示，需要插入一条数据: `db.test.insert({'test': 'test'})`
3. 然后执行`show dbs`就能看到此数据库了
4. 添加一个可读写操作的用户: `db.createUser({user:"用户名",pwd:"密码",roles:["readWrite"]})`

这样，在当前数据库下就会添加一个具有readWrite操作权限的用户了

这里要强调的是，需要在哪个库里添加用户，需要先执行 `use 数据库名`，进入当前数据库下，再执行`db.createUser`创建用户

## 权限说明

- dbOwner: 在当前db中执行任意操作
- readWrite: 读写数据权限
- read: 只读数据权限
