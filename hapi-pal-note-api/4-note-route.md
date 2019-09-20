# 4. สร้าง route สำหรับข้อมูล note

## 1. สร้างไฟล์ `lib/routes/note.js`

```js
'use strict';

module.exports = {
    method: '',
    path: '',
    options: {
        handler: async (request, h) => {}
    }
};
```

## 2. กำหนดรายละเอียดของ Route

กำหนด method, path, และ return JavaScript Object เป็น JSON ง่ายๆ 

```js
'use strict';

module.exports = {
    method: 'GET',
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