# 19. สร้าง test สำหรับกรณีที่ไม่มีข้อมูลส่งเข้ามาใน Route

เปิดไฟล์​ `test/note-save.test.js`

และเพิ่่ม test case เข้าไปอีก 2 ตัว

```js
it('Failed if post JSON has empty message', async () => {
        const inputPayload = {
            message: ''
        }


        const result = await server.inject({
            method:'post',
            url:'/notes',
            payload: inputPayload
        });

        expect(result.statusCode).to.not.equal(200);

    });

    it('Failed if post JSON has no message', async () => {
        const inputPayload = {}

        const result = await server.inject({
            method:'post',
            url:'/notes',
            payload: inputPayload
        });

        expect(result.statusCode).to.not.equal(200);

    });
```