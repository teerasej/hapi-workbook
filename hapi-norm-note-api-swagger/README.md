
# Note API with Swagger 

## Setup

1. [Setup](1-setup.md)

## สร้าง และใช้งาน Server Method

2. [สร้าง Server Method แยกส่วน business logic ออกมาจาก Route](2-server-method-get-all-note.md)
3. [เขียน test ให้กับ Route Note Get All](3-test-route-note-get-all.md)

## Save Note: สร้าง Route และ Server method

4. [สร้าง test suite สำหรับ save note route](4-route-save-note.md)
5. [สร้าง server method `saveNote`](5-server-method-save-note.md)
6. [สร้าง saveNote route](6-route-save-note.md)

## ใช้งาน Joi ในการ validate ข้อมูล

> [Joi API](https://github.com/hapijs/joi/blob/master/API.md)

7. [เขียน test ในกรณีที่การทำงานของ Save Note Route รับข้อมูลไม่ถูกต้อง](7-test-save-note-failed.md)
8. [ใช้ joi กำหนด schema input](8-validate-route-input-joi.md)
9. [แยกส่วนของการสร้าง DB client ออกมาเป็น helper](9-db-helper.md)
10. [เขียน test สำหรับ server.method saveNote](10-test-server-method-savenote.md)
11. [ใช้ joi validate ค่า input ของ server.method saveNote](11-joi-validate-input.md)

## กำหนดและใช้งาน Plugin

> [Hapi Swagger](https://github.com/glennjones/hapi-swagger)

12. [ตั้งค่า และเพิ่ม Swagger Plugin ลง server](12-setup-swagger.md)
13. [สลับ @hapi/joi มาใช้ joi module](13-switch-to-joi.md)
14. [ใส่รายละเอียดสำหรับ swagger documentation](14-swagger-document-route.md)