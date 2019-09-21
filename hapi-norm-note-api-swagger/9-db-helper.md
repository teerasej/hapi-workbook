
# 9. แยกส่วนของการสร้าง DB client ออกมาเป็น helper

## 1. สร้าง helper file

สร้างไฟล์ `lib/helpers/DB.js`

```js
const MongoClient = require('mongodb').MongoClient;
const uri = "mongodb+srv://username:password@sandbox1-wkmdm.mongodb.net/noteDB?retryWrites=true&w=majority";
const client = new MongoClient(uri, { useNewUrlParser: true });

module.exports = client; 
```

## 2. แก้ไขไฟล์ `loadAllNotes.js`

เปิดไฟล์ `lib/services/notes/loadAllNotes.js`

```js
'use strict';

// ใช้ module จาก helper แทน
const client = require('../../helpers/DB');

const loadAllNotes = async () => {
    const connection = await client.connect();
```

## 3. แก้ไขไฟล์ `saveNote.js`

เปิดไฟล์ `lib/services/notes/saveNote.js`

```js
'use strict';

// ใช้ module จาก helper แทน
const client = require('../../helpers/DB');

const saveNote = async () => {
    const connection = await client.connect();
```


