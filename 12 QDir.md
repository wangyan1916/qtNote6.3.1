`QDir `对目录结构及其内容的访问

```c++
#include <QDir>
#include <QDebug>
int main(int argc, char *argv[])
{
    QDir dir;
    dir.setFilter(QDir::Files | QDir::Hidden | QDir::NoSymLinks);
    dir.setSorting(QDir::Size | QDir::Reversed);
    // 返回目录中所有文件和目录的QFileInfo 对象列表
    QFileInfoList list = dir.entryInfoList();

    qDebug() << "Bytes Filename";
    for (auto &fileInfo :list) {
        qDebug()<<QString("%1%2").arg(fileInfo.size(), 10).arg(fileInfo.fileName());
    }

}

```

总结，这里的范围for用的是取地址符



```c++
#include <QDir>
#include <QDebug>
int main(int argc, char *argv[])
{
    QDir dir;
    if (dir.mkdir("mydir"))
        qDebug() << "mydir successfully created";
    dir.mkdir("mydir2");
    if (dir.exists("mydir2"))
        dir.rename("mydir2", "newdir");
    dir.mkpath("temp/newdir");

}

```

总结，创建文件夹或者直接创建路径下的文件夹

`QDir`的静态函数

```
current()
home()
root()
temp()
```



