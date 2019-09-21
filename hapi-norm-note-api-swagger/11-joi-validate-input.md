# 11. ใช้ joi validate ค่า input ของ server.method saveNote

เปิดไฟล์ `lib/services/notes/saveNote.js`

```js
const Joi = require('@hapi/joi');

const saveNote = async (message) => {

    // การเรียกใช้ Joi จะคืนค่ามาเป็น object ที่เรียกว่า Schema
    const schema = Joi.string().required().min(1);
    // สามารถเรียกใช้ fucntion `validate` ได้
    const { error } = schema.validate(message);

    // เช็คค่า error ที่ส่งกลับมาจาก validate
    if (error) {
        return { error }
    }

    //...
```