
# 7. เขียน test ในกรณีที่การทำงานของ Save Note Route รับข้อมูลไม่ถูกต้อง

## 1. เขียน test ที่ต้อง failed

เปิดไฟล์ `test/note-save.test.js`

และเพิ่ม test 

```js
it('Failed if post JSON has empty message', async () => {
        const inputPayload = {
            message: ''
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

        expect(result.statusCode).to.not.equal(200);

    });

    it('Failed if post JSON has no message', async () => {
        const inputPayload = {}

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

        expect(result.statusCode).to.not.equal(200);

    });
```