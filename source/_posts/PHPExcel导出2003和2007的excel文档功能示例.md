---
title: PHPExcel导出2003和2007的excel文档功能示例
date: 2018-05-07 15:27:18
categories: PHP
tags: [PHP,Excel]
---
今天公司要求做个php导出excel的程序，利用PHPExcel导出2003和2007的excel文档功能。
<!-- more -->

#### 本文实例讲述了PHPExcel导出2003和2007的excel文档功能。分享给大家供大家参考，具体如下：

```
include __DIR__ . '/classes/PHPExcel.php';
include __DIR__ .'/classes/PHPExcel/Writer/Excel2007.php';
include __DIR__ . '/classes/PHPExcel/Writer/Excel5.php';
include __DIR__ . '/classes/PHPExcel/IOFactory.php';
$objExcel = new PHPExcel();
//设置属性 (这段代码无关紧要，其中的内容可以替换为你需要的)
$objExcel->getProperties()->setCreator("andy");
$objExcel->getProperties()->setLastModifiedBy("andy");
$objExcel->getProperties()->setTitle("Office 2003 XLS Test Document");
$objExcel->getProperties()->setSubject("Office 2003 XLS Test Document");
$objExcel->getProperties()->setDescription("Test document for Office 2003 XLS, generated using PHP classes.");
$objExcel->getProperties()->setKeywords("office 2003 openxml php");
$objExcel->getProperties()->setCategory("Test result file");
$objExcel->setActiveSheetIndex(0);
$i=0;
//表头
$k1="编号";
$k2="用户名";
$k3="手机号";
$objExcel->getActiveSheet()->setCellValue('a1', "$k1");
$objExcel->getActiveSheet()->setCellValue('b1', "$k2");
$objExcel->getActiveSheet()->setCellValue('c1', "$k3");
//debug($links_list);
foreach($info as $k=>$v) {
$u1=$i+2;
/*----------写入内容-------------*/
$objExcel->getActiveSheet()->setCellValue('a'.$u1, $v["userid"]);
$objExcel->getActiveSheet()->setCellValue('b'.$u1, $v["username"]);
$objExcel->getActiveSheet()->setCellValue('c'.$u1, $v["mobile"]);
$i++;
}
// 高置列的宽度
$objExcel->getActiveSheet()->getColumnDimension('A')->setWidth(10);
$objExcel->getActiveSheet()->getColumnDimension('B')->setWidth(15);
$objExcel->getActiveSheet()->getColumnDimension('C')->setWidth(20);
$objExcel->getActiveSheet()->getHeaderFooter()->setOddHeader('&L&BPersonal cash register&RPrinted on &D');
$objExcel->getActiveSheet()->getHeaderFooter()->setOddFooter('&L&B' . $objExcel->getProperties()->getTitle() . '&RPage &P of &N');
// 设置页方向和规模
$objExcel->getActiveSheet()->getPageSetup()->setOrientation(PHPExcel_Worksheet_PageSetup::ORIENTATION_PORTRAIT);
$objExcel->getActiveSheet()->getPageSetup()->setPaperSize(PHPExcel_Worksheet_PageSetup::PAPERSIZE_A4);
$objExcel->setActiveSheetIndex(0);
$timestamp = time();
$ex='2007';
if($ex == '2007') { //导出excel2007文档
header('Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet');
header('Content-Disposition: attachment;filename="user'.$timestamp.'.xlsx"');
header('Cache-Control: max-age=0');
$objWriter = PHPExcel_IOFactory::createWriter($objExcel, 'Excel2007');
$objWriter->save('php://output');
exit;
} else { //导出excel2003文档
header('Content-Type: application/vnd.ms-excel');
header('Content-Disposition: attachment;filename="links_out'.$timestamp.'.xls"');
header('Cache-Control: max-age=0');
$objWriter = PHPExcel_IOFactory::createWriter($objExcel, 'Excel5');
$objWriter->save('php://output');
exit;
}
```
#### 另外还运用到txt文件逐行读取
```
$file = fopen("mobile.txt", "r");
$user=array();
$info=array();
$i=0;
while(! feof($file))
{
$user[$i]= fgets($file);//fgets()函数从文件指针中读取一行
$i++;
}
fclose($file);
```