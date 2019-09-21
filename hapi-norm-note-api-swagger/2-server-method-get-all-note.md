
# 2. สร้าง Server Method แยกส่วน business logic ออกมาจาก Route

## 1. สร้างไฟล์ server method

สร้างไฟล์ `lib/services/notes/loadAllNotes.js`

```js
'use strict';

const MongoClient = require('mongodb').MongoClient;
const uri = "mongodb+srv://<username>:<password>@sandbox1-wkmdm.mongodb.net/noteDB?retryWrites=true&w=majority";
const client = new MongoClient(uri, { useNewUrlParser: true });

// สร้าง function ที่ไว้ใช้เรียกข้อมูลจาก server
const loadAllNotes = async () => {
    const connection = await client.connect();
    const db = connection.db('noteDB');
    const collection = db.collection('notes');

    const result = await collection.find({}).toArray();
    console.log(result);

    return result;
}

// Export object เพื่อเอาไปใส่ใน server.method()
module.exports = {
    name: 'loadAll',
    method: loadAllNotes,
    options: {}
};

```

## 2. เพิ่ม loadAll ไว้ใน `server.method()`

เปิดไฟล์ `lib/server.js`

เริ่มจาก import เข้ามา และเพิ่มเข้าไปใน `server.method()`

```js
const methodLoadAllNotes = require('./services/notes/loadAllNotes');

//...

server.method(methodLoadAllNotes);

```

## 3. เรียกใช้งาน `server.methods()` ใน Route

เปิดไฟล์ `lib/routes/notes/note.getall.route.js`

และแก้ไขให้ handler function เรียกใช้ server method

```js
module.exports = {
    path: '/notes',
    method: 'GET',
    // เรียกใช้ server.methods() ผ่าน request object
    handler: async (request, h) => {
        return await request.server.methods.loadAll();;
    }
}; 
```