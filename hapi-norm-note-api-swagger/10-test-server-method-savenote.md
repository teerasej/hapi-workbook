
# 10. เขียน test สำหรับ server method saveNote

## 1. สร้างไฟล์ test

สร้างไฟล์ `lib/services/notes/saveNote.test.js`

```js
const { expect } = require('@hapi/code');
const saveNote = require('./saveNote');
const sinon = require('sinon');

describe('SaveNote Method', () => {

    beforeEach(async () => {
        
    })

    afterEach(async () => {
       
    })
});
```

## 2. test กรณีที่สำเร็จ

```js

    it('test Save Note', async () => {

        const mockMessage = 'test';

        let stubSaveNote = sinon.stub(saveNote,'method');
        stubSaveNote.onFirstCall().returns({ title: mockMessage, _id: 1 });

        let result = await saveNote.method(mockMessage);

        expect(result.title).to.equal(mockMessage);
        expect(result._id).to.exist();

        sinon.restore();
    });
```

## 3. เขียน test ที่ต้องคืนค่า error ถ้าค่าที่ส่งเป็น undefined หรือ empty string

```js
it('failed if undefined message', async () => {

        const mockMessage = undefined;

        let result = await saveNote.method(mockMessage);

        expect(result.error).to.exist();
    });

    it('failed if message is empty', async () => {

        const mockMessage = '';

        let result = await saveNote.method(mockMessage);

        expect(result.error).to.exist();
    });
```
