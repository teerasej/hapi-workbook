# 8. ใช้ joi กำหนด schema input

เปิดไฟล์ `lib/routes/notes/note.save.route.js`

ทำการ import joi module และกำหนดลงในส่วนของ `route.options.validate`

```js
const Joi = require('@hapi/joi');

module.exports = {
    method: 'post',
    path: '/notes',
    // แทนที่จะกำหนดเป็น handler อย่างเดียว ก็กำหนดเป็น options ได้ จะได้ตั้งค่าอื่นๆ ให้ route ด้วย เช่น การ validate
    options: {
        // นี่คือส่วนที่เพิ่มเข้าไป
        validate: {
            payload: Joi.object().keys({
                message: Joi.string().required().min(1)
            })
        },
        // ด้านล่างนี่คือ handler function ตัวเดิม
        handler: async (request, h) => {
```
