SQL injection vulnerability exists in ibos oa v4.5.5

official website:http://www.ibos.com.cn/

version :4.5.5

1. Log in to the background and go to the Integrated Office => Bulletin => Information Center => Delete packet capture

![WPS图片(1)](https://github.com/jack-521/cve/assets/138577927/bcf42b7c-a1f5-4b62-8d7c-d901edd853d8)

![WPS图片(2)](https://github.com/jack-521/cve/assets/138577927/bedd6fba-891e-4510-af72-eb0634d8caf6)

![WPS图片(3)](https://github.com/jack-521/cve/assets/138577927/5326489d-0932-40d6-bf39-b5cf1394c1fc)

2.Find the corresponding code through the route for analysis. The following are all api controllers

![WPS图片(4)](https://github.com/jack-521/cve/assets/138577927/edbfa7e2-b82b-4105-b222-db99edfe109c)

3. Enter the run() method of delete.php, receive incoming parameters through POST, and use $noDelete to check whether there is an unauthorized operation. When $noDelete is empty, enter the deleteByRelateid() method to execute sql statements and delete records.

![WPS图片(5)](https://github.com/jack-521/cve/assets/138577927/be44133f-4804-4292-9d44-f1cc4db20074)

$relateid is the articleids passed by the POST, and the query conditions are concatenated one by one after entering the deleteByRelateid() method

![WPS图片(6)](https://github.com/jack-521/cve/assets/138577927/b98dc12d-edc9-4b69-a9b8-b3dad23a0042)

The complete sql statement is concatenated by the createDeleteCommand() method of the YII framework

![WPS图片(7)](https://github.com/jack-521/cve/assets/138577927/e1d4230c-6a4b-4bdd-bf4e-4829c1cb6a26)

![WPS图片(8)](https://github.com/jack-521/cve/assets/138577927/987ba848-59b1-49ce-a8ad-ba64463d7729)

![WPS图片(9)](https://github.com/jack-521/cve/assets/138577927/15b80431-c903-4f0c-8a3f-8ec1f2a33547)

