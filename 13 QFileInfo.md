  

```c++
#include <QDir>
#include <QFileInfo>
#include <QDirIterator>
#include <QDebug>

int main(int argc, char *argv[])
{
    QDir dir{QDir::current()};
    dir.setFilter(QDir::Files | QDir:: AllDirs);

    qDebug()<< QString("Filename").leftJustified(30).append("Bytes");
    QDirIterator it(dir);
    while (it.hasNext()) {
        QFileInfo fileInfo = it.nextFileInfo();
        QString str = fileInfo.fileName().leftJustified(30);
        str.append(QString("%1").arg(fileInfo.size()));
        qDebug() << str;
    }
}

```

总结，这里有个java风格的迭代器