# 18. สร้าง route สำหรับ save note

ใช้คำสั่ง `npx hpal make route notes/save`

```js
'use strict';

module.exports = {
    method: 'post',
    path: '/notes',
    options: {
        handler: async (request, h) => {

            const message = request.payload.message;

            const { noteService } = request.services();

            return noteService.save(message);
        }
    }
};
```