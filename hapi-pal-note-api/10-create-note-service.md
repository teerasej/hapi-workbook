# 10. สร้างและจัดการ Note Service

## 1. สร้างไฟล์​

ใช้คำสั่ง `npx hpal make service note`

## 2. ให้ service เป็นคน return Array แทน

เปิดไฟล์ `lib/services/note.js`

```js
'use strict';

const Schmervice = require('schmervice');

module.exports = class NoteService extends Schmervice.Service {

    loadAll() {
        return [
            { title: 'bravo' },
            { title: 'tango' },
            { title: 'bobby' }
        ]
    }

};
```

## 3. ให้ Route เป็นคนขอข้อมูลจาก service แทน

เปิดไฟล์ `lib/routes/notes/get-all.js` 

```js
'use strict';

module.exports = {
    method: 'get',
    path: '/notes',
    options: {
        handler: async (request, h) => {

            const { noteService } = request.services();

            return noteService.loadAll();
        }
    }
};
```

## 4. ทดสอบรัน Test 