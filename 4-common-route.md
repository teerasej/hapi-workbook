
# 4. สร้าง Route 

## 1. สร้าง Route ใหม่ด้วย `server.route()`

เปิดไฟล์ `index.js`

ใช้ method `server.route` โดยกำหนด options (JavaScript Object) ลงไป

- **method**: ประเภทของ Request ที่รับกับ Route นี้
- **path**: URL path 
- **handler**: function ที่รับ request และ return ค่ากลับออกไปเป็น response ให้ client 

```js
// สร้าง route โดยใช้ JavaScript object 
server.route({
        method: 'GET',
        path:'/',
        handler: (request, h) => {
            return 'Hello ok!';

            // คืนค่าเป็น JSON
            // return { message: 'hello ok' }
        }
    });
```

## 2. ทดสอบการทำงาน

## ไฟล์ index.js

```js
`use strict`;
const Hapi = require('@hapi/hapi');

const init = async () => {

    const server = Hapi.server({
        port: 3000,
        host: 'localhost'
    });

    server.route({
        method: 'GET',
        path:'/',
        handler: (request, h) => {
            return 'Hello ok!';
        }
    });

    await server.start();
    console.log('Server running on %s', server.info.uri);
};

process.on('unhandledRejection', (err) => {

    console.log(err);
    process.exit(1);
});

init();
```