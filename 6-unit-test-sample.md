
# 6. สร้าง Unit Test แบบง่าย

## สร้างไฟล์ test

สร้างไฟล์ `test/example.test.js`

และ import module ต่างๆ ที่จำเป็นเข้ามา

```js
'use strict';

const Lab = require('@hapi/lab');
const { expect } = require('@hapi/code');
const { afterEach, beforeEach, describe, it } = exports.lab = Lab.script();
```

### ** สำหรับคนที่เคยใช้ Jest 

Lab กับ Code module ของ Hapi มีความคล้ายกัน กับ Mocha, Jest และ Chai แต่ถูกปรับแต่งให้เข้ากับการใช้งานบน Hapi มากขึ้น 

ดังนั้นจะเปรียบได้ง่ายๆ แบบนี้

- Lab = Jest, Mocha
- Code = Chai, Jest assertion

ขึ้นอยู่กับสถานการณ์และการใช้งาน สามารถสลับไปมาได้ 

## 2. import `init()` มาจาก server.js

เพราะตามที่ออกแบบไว้ init จะสร้างแต่ server instance แต่ไม่ได้รันใช้งานเป็น server จริงๆ 

```js
const { init } = require('../lib/server');
```

## 3. สร้าง test group

```js
describe('GET /', () => {

}); 
```

## 4. กำหนดค่าของ server ให้พร้อมก่อนเริ่มรัน test case 

- เราสามารถเตรียม code ที่ต้องการรันก่อนที่ test case แต่ละตัวจะเริ่มทำงาน ด้วย `beforeEach()` 
- และเตรียม code ที่ต้องการรัน หลังจาก test case แต่ละตัวทำงานเสร็จแล้วด้วย `afterEach()`

```js
describe('GET /', () => {
    let server;

    beforeEach(async () => {
        server = await init();
    });

    afterEach(async () => {
        await server.stop();
    });

}
```

## 5. เขียน test case แรก

- เรามี `server.inject(options)` ที่ใส่ options ลงไปให้ server นำไปทำงานต่อได้ (จำลองเหมือนมี request ยิงเข้ามาใน route นั้นจริงๆ)
- ค่าที่ได้ออกมาคือ response จาก Route นั่นเอง
- วิธีการเขียน assertion ของ code จะแตกต่างจาก jest สามารถดูเพิ่มเติมได้ที่ [API Reference](https://github.com/hapijs/code/blob/master/API.md)

```js
describe('GET /', () => {
    let server;

    beforeEach(async () => {
        server = await init();
    });

    afterEach(async () => {
        await server.stop();
    });

    // สามารถเขียนได้เหมือนกับ test case อื่น
    it('responds with 200', async () => {
        const res = await server.inject({
            method: 'get',
            url: '/'
        });
        expect(res.statusCode).to.equal(200);
    });
}
```