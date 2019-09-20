# 6. ย้ายและ rename ไฟล์ ไปไว้ใน folder ของ notes

เป็นการจัดกลุ่ม route action ให้ทดสอบได้ง่าย

สร้างไฟล์ `lib/routes/notes/get-all.js`

```js
'use strict';

module.exports = {
    method: 'get',
    path: '/notes',
    options: {
        handler: async (request, h) => {
            return [
                { title: 'bravo' },
                { title: 'tango' },
                { title: 'bobby' }
            ]
        }
    }
};

```