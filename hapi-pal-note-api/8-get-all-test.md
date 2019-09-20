# 8. เขียน Test case ของ Get-all

## 1. สร้างไฟล์ test

รันคำสั่ง `npm test` หรือ `yarn test`

สร้างไฟล์ `test/get-all.test.js`

```js
const Lab = require('@hapi/lab');
const { expect } = require('@hapi/code');
const Server = require('../server');

describe('Note route', () => {

    it('GET All', () => {

    });

}); 
```

## 2. ตั้งค่าเรียกใช้ server ก่อนรัน test case

```js
const Lab = require('@hapi/lab');
const { expect } = require('@hapi/code');
const Server = require('../server');

describe('Note route', () => {
    
    // กำหนดตัวแปรเก็บ server ที่ใช้ทดสอบในแต่ละเคส
    let server;

    // เริ่มโค้ดของ server ก่อนเริ่มรัน 1 เคส
    beforeEach(async () => {
        server = await Server.deployment(false);
    });

    // หยุดการทำงานของ server ทุกครั้งที่รัน 1 เคสเสร็จ
    afterEach(async () => {
        await server.stop();
    });


    it('GET All', () => {
        
    });

});
```

## 3. test ทดสอบว่ามี url อยู่จริงตามที่กำหนด

```js
// test/get-all.test.js

it('GET All existed', async () => {
        const result = await server.inject({
            method:'get',
            url:'/notes'
        });

        expect(result.statusCode).to.equal(200);
    });
```

## 4. เขียน test อีกตัวเพื่อทดสอบ json ที่ return ออกมาเป็น Array

```js
// test/get-all.test.js

it('Got a load of notes', async () => {
        const result = await server.inject({
            method:'get',
            url:'/notes'
        });

        const resultJSON = JSON.parse(result.payload);
        expect(resultJSON).to.be.an.array();
    });
```

## 5. ทดสอบรัน test

## ไฟล์เต็ม