MOC（元对象编译器）Meta-Object Compiler,一个预处理器

使用MOC，要添加`Q_OBJECT`宏





QObjcet 不支持拷贝

```c++
#include <QCoreApplication>



class A:public QObject{
public:
    A(QObject *parent = nullptr);
    ~A();

};

A::A(QObject *parent):QObject(parent){
    qDebug()<<this<<"被构造";
}
A::~A(){
    qDebug() <<this <<"被销毁";
}

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);
    A objA;
    A *pA2 = new A(&objA);
    qDebug() << "objA2:" <<pA2;

//    return a.exec();
}

```

