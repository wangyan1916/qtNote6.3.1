`mian`函数

```c++
#include "widget.h"

#include <QApplication>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    Widget w;

    w.resize(250, 250);
    w.setWindowTitle("这是一个简单的例子");
    w.setToolTip("这是一个QWidget");

    w.show();

    return a.exec();
}

```

`QWiget`构造函数

```c++
#include "widget.h"
#include <QFrame>
#include <QGridLayout>
#include <QPushButton>
#include <QApplication>
Widget::Widget(QWidget *parent)
    : QWidget(parent)
{
    // 内容
    auto *frame1 = new QFrame(this);
    frame1->setFrameStyle(QFrame::Box);
    frame1->setCursor(Qt::SizeAllCursor);
    auto *frame2 = new QFrame(this);
    frame2->setFrameStyle(QFrame::Box);
    frame2->setCursor(Qt::WaitCursor);
    auto *frame3 = new QFrame(this);
    frame3->setFrameStyle(QFrame::Box);
    frame3->setCursor(Qt::PointingHandCursor);

    // 格式-布局
    auto *grid = new QGridLayout(this);
    grid->addWidget(frame1, 0, 0);
    grid->addWidget(frame2, 0, 1);
    grid->addWidget(frame3, 0, 2);

    QPushButton * butt = new QPushButton("quit", this);
    connect(butt, &QPushButton::clicked,
            qApp, &QApplication::quit);

    auto *grad2 = new QGridLayout(frame3);
    grad2->addWidget(butt);



}
```