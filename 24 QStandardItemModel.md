与`QTableView`组成`Model/View`

`QDataWidgetMapper`类允许在`widget`集合中查看和编辑从模型获得的信息

头文件略

源文件：

```c++
#include "mainwindow.h"
#include "./ui_mainwindow.h"
#include <QStandardItemModel>
#include <QDataWidgetMapper>
#include <QModelIndex>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    setFixedSize(365, 200);

    ui->setupUi(this);
    setWindowTitle("QStandarItemModel");
    setupModle();
    // 设置数据关联
    ui->tableView->setModel(model);
    // 根据内容改变表格宽度
    ui->tableView->horizontalHeader()->setSectionResizeMode(QHeaderView::ResizeToContents);
    // 设置表头
    QStringList headers = {"姓名", "电话", "年龄"};
    model->setHorizontalHeaderLabels(headers);
    // 数据与控件绑定
    mapper = new QDataWidgetMapper(this);
    mapper->setModel(model);
    mapper->addMapping(ui->nameEdit, 0);
    mapper->addMapping(ui->phoneEdit_2, 1);
    mapper->addMapping(ui->ageSpinBox, 2);

    // 做一个信号和槽的连接
    connect(ui->preBtn, &QPushButton::clicked,
            mapper, &QDataWidgetMapper::toPrevious);
    connect(ui->nextBtn, &QPushButton::clicked,
            mapper, &QDataWidgetMapper::toNext);
    connect(mapper, &QDataWidgetMapper::currentIndexChanged,
            this, &MainWindow::updateButtons);
    // 显示第一组
    mapper->toFirst();


}

MainWindow::~MainWindow()
{
    delete ui;
}

void MainWindow::setupModle()
{
   model = new QStandardItemModel(5, 3, this);
   QStringList names;
   names
           << "张三"
           << "李四"
           << "王五"
           << "丁一"
           << "柳儿";
   QStringList phoneNums;
   phoneNums
           << "17843102741"
           << "17843102742"
           << "17843102743"
           << "17843102744"
           << "17843102745";
   QStringList ages;
   ages
           << "20"
           << "10"
           << "30"
           << "40"
           << "50";


   for (int row = 0; row <5; ++row) {
       QStandardItem *item = new QStandardItem(names[row]);
       model->setItem(row, 0, item);

       item = new QStandardItem(phoneNums[row]);
       model->setItem(row, 1, item);

       item = new QStandardItem(ages[row]);
       model->setItem(row, 2, item);
   }
}

void MainWindow::updateButtons(int row)
{
    ui->preBtn->setEnabled(row > 0);
    ui->nextBtn->setEnabled(row<model->rowCount()-1);

    QModelIndex index = model->index(row, 0);
    ui->tableView->selectRow(index.row());

}


void MainWindow::on_tableView_clicked(const QModelIndex &index)
{
   mapper->setCurrentIndex(index.row());

}


```

总结，相当于多开一个修改表格的窗口，然后一些俩窗口间的联动，实际上可能不如直接在上面改方便