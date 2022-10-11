头文件

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

源文件

```c++
#include "minusplus.h"
#include <QPushButton>
#include <QGridLayout>
#include <QLabel>
MinusPlus::MinusPlus(QWidget *parent)
    : QWidget(parent)
{
    auto *plsBtn = new QPushButton("+", this);
    auto *minBtn = new QPushButton("-", this);
    lbl = new QLabel("0", this);

    auto *gird = new QGridLayout(this);
    gird->addWidget(plsBtn, 0, 0);
    gird->addWidget(minBtn, 0, 1);
    gird->addWidget(lbl, 1, 0);

    connect(plsBtn, &QPushButton::clicked, this, &MinusPlus::OnPlus);
    connect(minBtn, &QPushButton::clicked, this, &MinusPlus::OnMinus);
}

MinusPlus::~MinusPlus()
{
}

void MinusPlus::OnPlus()
{
    int val = lbl->text().toInt();
    lbl->setText(QString::number(++val));
}

void MinusPlus::OnMinus()
{
    int val = lbl->text().toInt();
    lbl->setText(QString::number(--val));
}

```

自定义槽函数已经基本上会使用了，相对而言没有理解的是对于类中的属性，定义和使用的问题。