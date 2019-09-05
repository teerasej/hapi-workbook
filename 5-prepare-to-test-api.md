
# การเขียน Test เบื้องต้น

การเขียน test เบื้องต้น สามารถทำได้เหมือนกับ Node project ทั่วไป 

แต่ Hapi จะมี module แนะนำที่ออกแบบมาเฉพาะอยู่แล้ว คือ **Lab** และ **code**

## 1. แยก code **รัน server** และ**สร้าง server** ออกจากกัน

ส่วนใหญ่แล้ว เมื่อต้องการเขียน test ให้ Hapi ด้วย เรามักแยก 2 ส่วนนี้ออกจากกัน 

1. ส่วนกำหนดการทำงานของ server
2. ส่วนเริ่มการทำงานของ server

ให้ทำการสร้างไฟล์ `lib/server.js` 

## 2. จากนั้นสร้าง server object ตามปกติ

```js
const Hapi = require('@hapi/hapi');

const server = Hapi.server({
    port: 3000,
    host: 'localhost'
});
```

## 3. กำหนด Route เบื้องต้นพองาม

```js

server.route({
  method: 'GET',
  path: '/',
  handler: function () {

      return 'hello ok!';
  }
});
```
## 4. สร้าง init และ start function 

เราจะ export function ชื่อ `init()` เพื่อตอนเรียกใช้ จะมีการสร้าง object ของ server ให้พร้อมใช้ 

**แต่ไม่ได้รันให้ server ทำงาน** 

ซึ่งจะเป็นประโยชน์ตอนเราต้องการ test ตัว server และการทำงานต่างๆ 

```js

exports.init = async () => {

    await server.initialize();
    return server;
};
```

เราจะ export function ชื่อ `start()` เพื่อตอนเรียกใช้ จะเป็นการเริ่มการทำงานของ server 

ในกรณีนี้ เราจะได้ server ที่รันทำงานตาม port และค่าต่างๆ ที่ตั้งไว้

```js
exports.start = async () => {

    await server.start();
    console.log(`Server running at: ${server.info.uri}`);
    return server;
};
```

## ไฟล์เต็ม `lib/server.js`

```js
const Hapi = require('@hapi/hapi');

const server = Hapi.server({
    port: 3000,
    host: 'localhost'
});

server.route({
  method: 'GET',
  path: '/',
  handler: function () {

      return 'Hello World!';
  }
});

exports.init = async () => {

    await server.initialize();
    return server;
};

exports.start = async () => {

    await server.start();
    console.log(`Server running at: ${server.info.uri}`);
    return server;
};

process.on('unhandledRejection', (err) => {

    console.log(err);
    process.exit(1);
}); 
```

## 5. เปลี่ยนไฟล์ `index.js` ให้รันการทำงานของ server

แก้ไขโค้ดในไฟล์​ `index.js` ให้เหลือแค่นี้

```js
// index.js
`use strict`;

const { start } = require('lib/server');

start();

```