widget 头文件

```c++
#ifndef WIDGET_H
#define WIDGET_H

#include <QWidget>

class Widget : public QWidget
{
    Q_OBJECT

public:
    Widget(QWidget *parent = nullptr);
    ~Widget();

    // QWidget interface
protected:
    void paintEvent(QPaintEvent *event) override;
};
#endif // WIDGET_H

```



widget 源文件

```c++
#include "widget.h"
#include <QtWidgets>
Widget::Widget(QWidget *parent)
    : QWidget(parent)
{
    QTimer *timer = new QTimer(this);
    connect(timer, &QTimer::timeout,
            this, QOverload<>::of(&Widget::update));
    timer->start(1000);
    resize(200,200);

}

Widget::~Widget()
{
}

void Widget::paintEvent(QPaintEvent *event)
{
    static const QPoint hourHand[3] = {QPoint(7, 8),
                                      QPoint(-7,8),
                                      QPoint (0, -40)};
    static const QPoint MinuteHand[3] = {
        QPoint(7, 8), QPoint(-7, 8), QPoint(0, -70)
    };
    static const QPoint secondHand[3] = {
        QPoint(4, 8), QPoint(-4, 8), QPoint(0, -85)
    };
    QColor hourColor(127, 0, 127);
    QColor minuteColor(0, 127, 127, 191);
    QColor secondColor(127, 127, 0, 100);


    QTime time = QTime::currentTime();

    QPainter painter(this);
    painter.setRenderHint(QPainter::Antialiasing);
    painter.translate(width()/2, height()/2);
    painter.setPen(Qt::NoPen);

    // 时针绘制
    painter.setBrush(hourColor);
    painter.save();
    painter.rotate(30*(time.hour()+time.minute()/60.0));
    painter.drawPolygon(hourHand, 3);
    painter.restore();
    // 分针绘制
    painter.setBrush(minuteColor);
    painter.save();
    painter.rotate(6*(time.minute()+time.second()/60));
    painter.drawPolygon(MinuteHand, 3);
    painter.restore();
    // 秒针绘制
    painter.setBrush(secondColor);
    painter.save();
    painter.rotate(6*time.second());
    painter.drawPolygon(secondHand, 3);
    painter.restore();

    // 表盘绘制
    for (int i=0; i<60; i++){
        if (!(i%5)) {
            painter.setPen(hourColor);
            painter.drawLine(90, 0, 96, 0);

        }else{
            painter.setPen(minuteColor);
            painter.drawLine(92, 0, 96, 0);
        }
        painter.rotate(6);
    }
    painter.restore();


}


```

main 文件

```c++
#include "widget.h"

#include <QApplication>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    Widget w;
    w.setWindowTitle("Sample Clock");
    w.resize(250, 250);
    w.show();

    return a.exec();
}

```

总结，`Qpaint`绘制，然后通过时间改变更新窗口