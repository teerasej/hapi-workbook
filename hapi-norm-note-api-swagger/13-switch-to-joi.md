
# 13. สลับ @hapi/joi มาใช้ joi module

เนื่องจาก hapi-swagger มีปัญหากับ @hapi/joi เราจำเป็นต้องสลับมาใช้ joi ปกติแทน

เปิดไฟล์ 
- `lib/routes/notes/note.save.route.js` 
- `lib/services/notes/saveNote.js`

แก้จาก

```js
- const Joi = require('@hapi/joi');
+ const Joi = require('joi');
```