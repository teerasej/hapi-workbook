
# 5. สร้าง server method `saveNote`

## 1. สร้าง server method file

สร้างไฟล์ `lib/services/notes/saveNote.js`

```js
'use strict';

const MongoClient = require('mongodb').MongoClient;
const uri = "mongodb+srv://username:password@sandbox1-wkmdm.mongodb.net/noteDB?retryWrites=true&w=majority";
const client = new MongoClient(uri, { useNewUrlParser: true });

const saveNote = async (message) => {
    let result;

    const connection = await client.connect();
    const db = connection.db('noteDB');
    const collection = db.collection('notes');

    result = await collection.insertOne({ title: message });
    client.close();
    return result.ops[0];
}


module.exports = {
    name: 'saveNote',
    method: saveNote,
    options: {}
};

```

## 2. เพิ่ม server method saveNote เข้า server 

เปิดไฟล์ ``

```js
const methodSaveNote = require('./services/notes/saveNote');

//...

server.method(methodLoadAllNotes);
server.method(methodSaveNote); // เพิ่มเข้าไปได้ จัดระเบียบดีๆ 
```