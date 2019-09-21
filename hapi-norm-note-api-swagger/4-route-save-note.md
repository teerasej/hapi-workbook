
# 4. สร้าง test suite สำหรับ save note route

## 1. สร้างไฟล์​ test

สร้างไฟล์ `test/note-save.test.js`

และกำหนดตัวแปรที่จะใช้ใน test case เช่น `server` และ `stub`

```js

const { expect } = require('@hapi/code');
const { init } = require('../lib/server');
const sinon = require('sinon');


describe('Note Save Operation', () => {

    let server;
    let stubSaveNote;

    beforeEach(async () => {
        server = await init();
        stubSaveNote = sinon.stub(server.methods, 'saveNote');
    });

    afterEach(async () => {
        sinon.restore();
        await server.stop();
    });

}); 
```

## 2. เขียน test ในกรณีที่ save สำเร็จ

```js
it('Save successful', async () => {

    const inputPayload = {
        message: 'Nextflow'
    }

    const successPayload = {
        _id: 1,
        title: 'Nextflow'
    }

    stubSaveNote.onFirstCall().returns(successPayload);

    const result = await server.inject({
        method:'post',
        url:'/notes',
        payload: inputPayload
    });

    expect(result.statusCode).to.equal(200);

    const resultJSON = JSON.parse(result.payload);
    expect(resultJSON).to.exist();
    expect(resultJSON._id).to.exist();
    expect(resultJSON.title).to.exist();
    expect(resultJSON.title).to.equal(successPayload.title);
});
```