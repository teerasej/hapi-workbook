# 12. ตั้งค่า และเพิ่ม Swagger Plugin

## 1. รันคำสั่งติดตั้ง 

```bash
npm install hapi-swagger @hapi/inert @hapi/vision
```
หรือ
```bash
yarn add hapi-swagger @hapi/inert @hapi/vision
```

## 3. import module 

เปิดไฟล์ `lib/server.js`

```js
const Inert = require('@hapi/inert');
const Vision = require('@hapi/vision');
const HapiSwagger = require('hapi-swagger');
// อ่านค่าจาก package.json โดยตรง
const Pack = require('../package.json');
```

## 4. ตั้งค่า options ให้ Swagger

```js
server.method(methodSaveNote);

// ถัดจากส่วนกำหนด server.method เราจะเริ่มเขียน options ให้ Swagger 
const swaggerOptions = {
    info: {
        title: 'Note API Documentation',
        // ดึงค่า version ในไฟล์ package.json มากำหนดให้ Swagger
        version: Pack.version,
    },
};
```

## 5. Register Plugin Swagger และที่จำเป็นเข้าระบบ server

ถัดลงมาเราจะเรียกใช้ `server.register([])` เพื่อระบุ plugin ที่ต้องการลงไปใน server 
 
```js
await server.register([
    Inert,
    Vision,
    {
        plugin: HapiSwagger,
        options: swaggerOptions
    }
]);
```

## 6. เขียนส่วนของ Setup ให้เป็น async function 

เพื่อให้การเรียกใช้ `await server.register` สามารถใช้งานได้ 

```js
// ครอบขั้นตอนการ setup server ทั้งหมดเป็น async function
const setup = async () => {
    const server = Hapi.server({
        port: 3000,
        host: 'localhost'
    });

    server.route(routeNoteSave);
    server.route(routeNoteGetAll);
    server.route(routeUserSignin);
    server.route(routeDefault);

    server.method(methodLoadAllNotes);
    server.method(methodSaveNote);

    const swaggerOptions = {
        info: {
            title: 'Test API Documentation',
            version: '1.0',
        },
    };


    await server.register([
        Inert,
        Vision,
        {
            plugin: HapiSwagger,
            options: swaggerOptions
        }
    ]);

    return server;

}




exports.init = async () => {

    // ใช้ค่า server ที่ได้จาก function setup() แทน
    let server = await setup();

    await server.initialize();
    return server;
}

exports.start = async () => {

    // ใช้ค่า server ที่ได้จาก function setup() แทน
    let server = await setup();

    await server.start();
    console.log(`Server running at: ${server.info.uri}`);
    return server;
}
```
