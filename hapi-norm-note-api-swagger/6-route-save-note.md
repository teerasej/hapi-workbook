
# 6. สร้าง saveNote route

## 1. สร้างไฟล์​ route 

สร้างไฟล์​ `lib/routes/notes/note.save.route.js`

```js
module.exports = {
    method: 'post',
    path: '/notes',
    options: {
        handler: async (request, h) => {

            // ดึงค่า message ออกมาจาก payload (ในที่นี้คือ json ที่ส่งมาจาก client)
            const message = request.payload.message;
            
            // เรียกใช้ server method
            return await request.server.methods.saveNote(message);
        }
    }
}; 
```

## 2. เพิ่ม Route เข้า server

เปิดไฟล์​ `lib/server.js`

```js
const routeNoteSave = require('./routes/notes/note.save.route');

//.. 

server.route(routeNoteSave);
```