# 22. เขียน test failed ถ้าใส่ undefined หรือ empty string

เปิดไฟล์ `test/note.test.js`

เราจะเพิ่มเข้าไปอีก 2 test case ดังนี้ 

```js
it('failed if undefined message', async () => {

        const mockMessage = undefined;

        const service = new NoteService();
        let result = await service.save(mockMessage);

        expect(result.error).to.exist();
    });

    it('failed if message is empty', async () => {

        const mockMessage = '';

        const service = new NoteService();
        let result = await service.save(mockMessage);

        expect(result.error).to.exist();
    });
```