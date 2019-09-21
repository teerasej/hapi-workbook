# 14. ใส่รายละเอียดสำหรับ swagger documentation

เปิดไฟล์ `lib/routes/default.js`

```js
module.exports = {
    method:'get',
    path: '/',
    // ของเก่า
    // handler: (request) => {
    //    return {
    //        message: 'hello'
    //    };
    // แก้เป็น options และใส่รายละเอียดสำหรับ Swagger
    options: {
        description: 'Default route',
        notes: 'helloooooo.....',
        tags: ['api'], 
        handler: (request) => {
            return {
                token: '1234567890'
            }
        }
    }
} 
```

เปิดไฟล์ `lib/routes/notes/note.getall.route.js`

```js
module.exports = {
    path: '/notes',
    method: 'GET',
    // handler: async (request, h) => {
    //     return await request.server.methods.loadAll();
    options: {
        description: 'Get All Notes',
        notes: 'Get all notes from database',
        tags: ['api'], 
        handler: async (request, h) => {
            return await request.server.methods.loadAll();;
        }
    }
}; 
```

เปิดไฟล์ `lib/routes/notes/note.save.route.js`

เพิ่มค่าเข้าไปใน options

```js
options: {
        description: 'Save Note',
        notes: 'Save message to DB',
        tags: ['api'], 
```
