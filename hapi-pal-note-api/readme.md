
# Note API with Hapi Pal

## 1. Configuration 

1. [สร้างโปรเจค](1-create-project.md) 
2. [Configuration-oriented Project](2-knowing-configuration.md)

## 2. Route

> [HapiPal](https://hapipal.com/getting-started)
> [HauteCouture API](https://github.com/hapipal/haute-couture) 

3. [สร้าง Starter Route ด้วย Hapi Pal](3-starer-route-with-hpal.md)
4. [สร้าง route สำหรับข้อมูล note](4-note-route.md)
5. [กำหนดค่า module **HauteCouture**](5-config-hc.md)
6. [ย้ายและ rename ไฟล์ ไปไว้ใน folder ของ notes](6-move-route-file.md)

## 3. Testing 

> [Jest Documentation](https://jestjs.io/)

7. [ติดตั้ง และตั้งค่า jest](7-setup-jest.md)
8. [เขียน Test case ของ Get-all](8-get-all-test.md)

## 4. Service 

> [Schemervice Documentation](https://github.com/hapipal/schmervice)

9. [ติดตั้ง และตั้งค่า Service (schemervice)](9-setup-schmervice.md)
10. [สร้างและจัดการ Note Service](10-create-note-service.md)

## 5. MongoDB

> [MongoDB Node API](https://mongodb.github.io/node-mongodb-native/contents.html)

11. [Setup](11-setup-mongodb.md)
12. [เชื่อมต่อฐานข้อมูล MongoDB](12-connect-database.md)
13. [ปรับการ test](13-test-timeout.md)

## 6. Sinon Test

> [Sinon Documentation](https://sinonjs.org/)

14. [ติดตั้ง Sinon](14-setup-sinon.md) 
15. [ใช้งาน Sinon ใน Test](15-using-sinon.md)

## 7. Save Note Route

ส่วนนี้ให้รัน jest ไปด้วยนะครับ

16. [สร้าง test unit สำหรับ save note](16-save-note-test.md)
17. [สร้าง save method ใน Note Service](17-create-save-method.md)
18. [สร้าง route สำหรับ save note](18-save-note-route.md)
19. [สร้าง test สำหรับกรณีที่ไม่มีข้อมูลส่งเข้ามาใน Route](19-test-note-failed.md)

## 8. Joi Validation

> [Joi API](https://github.com/hapijs/joi/blob/master/API.md)

20. [Validate ค่าที่ส่งเข้ามาทาง request ด้วย Joi](20-joi-validate-route-payload.md)
21. [เขียน test ให้ NoteService.save()](21-test-note-service-save.md)
22. [เขียน test failed ถ้าใส่ undefined หรือ empty string](22-failed-if-empty-string.md)
23. [ใช้ joi validate ข้อมูลใน service](23-joi-validate-service-data.md)
