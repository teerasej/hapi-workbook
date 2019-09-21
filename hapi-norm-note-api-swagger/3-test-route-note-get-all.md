
# 3. เขียน test ให้กับ Route Note Get All

## 1. สร้าง Test file

สร้างไฟล์ `test/note.get.all.route.test.js`

ทำการ import module ที่ต้องการใช้งาน

```js
const sinon = require('sinon');
const { expect } = require('@hapi/code');
const { init } = require('../lib/server');
```

## 2. เขียน test case

ในที่นี้เราจะมีการใช้ `sinon.stub` เพื่อจำลองการทำงานของ `server.methods` ที่ชื่อว่า `loadAll` ด้วย

```js
describe('Note route', () => {

    let server;
    let stubLoadAll;

    beforeEach(async () => {
       server = await init(false);

       // stub server.methods ที่ชื่อว่า loadAll
       stubLoadAll = sinon.stub(server.methods, 'loadAll');
    });

    afterEach(async () => {
       // รีเซ็ตการทำงานของ sinon ทุกครั้งที่รัน test แต่ละตัวเสร็จ
       sinon.restore();
       await server.stop();
    });

    it('GET All exists', async () => {

        // จำลองค่าที่ return ออกมาจาก server.methods.loadAll() ครั้งแรกเป็น []
        stubLoadAll.onFirstCall().returns([]);

        const result = await server.inject({
            method:'get',
            url:'/notes'
        });

        expect(result.statusCode).to.equal(200);

    });

    it('Got json a load of notes', async () => {

        let mockNotes = [
            { title: 'hello' },
            { title: 'world' }
        ];

        // จำลองค่าที่ return ออกมาจาก server.methods.loadAll() ครั้งแรกเป็นค่าที่จำลองไว้
        stubLoadAll.onFirstCall().returns(mockNotes);

        const result = await server.inject({
            method:'get',
            url:'/notes'
        });

        const resultJSON = JSON.parse(result.payload);
        expect(resultJSON).to.exist();
        expect(resultJSON).to.be.an.array();

    });

});
```