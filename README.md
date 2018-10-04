# database-in-python
import sqlite3

connect = sqlite3.connect('test.db')
cursor = connect.cursor()                   #创建游标，以便使用sql语句

#创建一个名为diary的表，并设置一个id为自增主键，title、content为text类型
cursor.execute('CREATE TABLE diary(id INTEGER PRIMARY KEY AUTOINCREMENT,title TEXT,content TEXT)')

#向表中插入数据，因为是自增主键，id可以写为NUll，表中id值会是123，递增
cursor.execute("INSERT INTO diary VALUES(NULL,'title1','content1')")

#或者也可以这样写：
cursor.execute("INSERT INTO diary(title,content) VALUES('title2','content2')")
#查询表中所有数据，并输出
for row in cursor.execute("SELECT*FROM diary"):
    print(row)
print('*****增*****\n')

#删除表中id为1的数据
cursor.execute("DELETE FROM diary WHERE id=1")
for row in cursor.execute("SELECT *FROM diary"):
    print(row)
print('删除')

#修改
cursor.execute("UPDATE diary SET title ='title',content='content' WHERE id = 2")
for row in cursor.execute("SELECT *FROM diary"):
    print(row)
print('修改')

items=[("title0","comtemt0"),("title1","comtemt1"),("title2","content2")]
#executemary一次向标准插入多条数据
cursor.executemany("INSERT INTO diary(title,content) VALUES(7,7)",items)
print("插入多条数据后的表：")
for row in cursor.execute("SELECT *FROM diary"):
    print(row)

print("查id为5 的数据：")
cursor.excute("SELECT*FROM diary WHERE id = 5")
print(cursor.fetchall())

print("查title为0 的数据：")
cursor.excute("SELECT*FROM diary WHERE title = 'title0'")
print(cursor.fetchall())

cursor.close()
connect.close()
