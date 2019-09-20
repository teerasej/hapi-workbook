15. ใช้งาน Sinon ใน Test

## 1. โหลด sinon และ NoteService เพื่อเตรียมการทำ stub

อย่าลืมรันเทสเปิดไว้

เปิดไฟล์ `test/get-all.test.js`

```js
// เรียกใช้ sinon
const sinon = require('sinon');
// เราจะทำการ sinon noteService 
const NoteService = require('../lib/services/note');
```

## 2. สร้าง stub ของ NoteService.loadAll

ในช่วงก่อนเริ่มเทส และ restore sinon ให้พร้อมทุกครั้งที่
รัน case แต่ละอันเสร็จ

```js
describe('Note route', () => {

    let server;
    let stubLoadAll;

    beforeEach(async () => {
        server = await Server.deployment(false);
        stubLoadAll = sinon.stub(NoteService.prototype, 'loadAll');
    });

    afterEach(async () => {
        sinon.restore();
        await server.stop();
    });
```

## 3. จำลองการเรียก loadAll ครั้งแรก

โดยกำหนดค่าที่ควรจะถูก return ออกมาอย่างที่ควรจะเป็น 

```js
    it('Got a load of notes', async () => {

        jest.setTimeout(30000);

        const mockNotes = [
            {title:'a'},
            {title:'b'},
            {title:'c'}
        ]
        stubLoadAll.onFirstCall().returns(mockNotes);


        const result = await server.inject({
            method:'get',
            url:'/notes'
        });

        const resultJSON = JSON.parse(result.payload);
        expect(resultJSON).to.be.an.array();
        expect(resultJSON.length).to.equal(3);
    });
```

## 4. จำลองการเรียก loadAll คืนค่าเป็น array เปล่า

```js
it('GET All existed', async () => {

        jest.setTimeout(30000);

        stubLoadAll.onFirstCall().returns([]);

        const result = await server.inject({
            method:'get',
            url:'/notes'
        });

        expect(result.statusCode).to.equal(200);
});
```