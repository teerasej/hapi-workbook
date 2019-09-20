# 20. Validate ค่าที่ส่งเข้ามาทาง request ด้วย Joi 

เปิดไฟล์ `lib/routes/notes/save.js`

```js
'use strict';

// require Joi module
const Joi = require('@hapi/joi');

module.exports = {
    method: 'post',
    path: '/notes',
    options: {
        // เพิ่มค่า validate เข้าไปใน options
        // กำหนดให้ validate ส่วนของ payload (แน่นอนว่าสามารถใช้กับ params หรือ header ได้ด้วย)
        validate: {
            payload: {
                // กำหนดในส่วนของ json payload ต้องมีค่า message และเป็น string ความยาวอย่างน้อย 1 ตัวอักษร
                message: Joi.string().required().min(1)
            }
        },
        handler: async (request, h) => {

            const message = request.payload.message;

            const { noteService } = request.services();

            return noteService.save(message);
        }
    }
};
```

## รัน test ล่าสุดทดสอบ