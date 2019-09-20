# 12. เชื่อมต่อฐานข้อมูล MongoDB

## 1. เรียกใช้ MongoDB ใน Service

เปิดไฟล์ `lib/services/note.js`

เริ่มจาก import และกำหนด URI ก่อน (ในที่นี้ใช้ของ Mongo Atlas)

```js
'use strict';

const Schmervice = require('schmervice');

// ส่วนที่เขียนขึ้นมา
const MongoClient = require('mongodb').MongoClient;
const uri = "mongodb+srv://<Username>:<Password></Password>@sandbox1-wkmdm.mongodb.net/noteDB?retryWrites=true&w=majority";
const client = new MongoClient(uri, { useNewUrlParser: true });
```

แทนที่ข้อมูล Array ด้วยการเขียนเรียกข้อมูลจาก Database

```js
async loadAll() {

        let result;

        const connection = await client.connect();
        const db = connection.db('noteDB');
        const collection = db.collection("notes");

        result = await collection.find({}).toArray();
        console.log(result);
        return result;

        // return [
        //     { title: 'bravo' },
        //     { title: 'tango' },
        //     { title: 'bobby' }
        // ]
}
```

## 2. ปรับให้ Route ใช้งานข้อมูลจาก Service 

เปิดไฟล์ `lib/routes/notes/get-all.js`

```js
'use strict';

module.exports = {
    method: 'get',
    path: '/notes',
    options: {
        handler: async (request, h) => {

            const { noteService } = request.services();

            return await noteService.loadAll();
        }
    }
};
```

## ไฟล์เต็ม `lib/services/note.js`

```js
'use strict';

const Schmervice = require('schmervice');
const MongoClient = require('mongodb').MongoClient;
const uri = "mongodb+srv://note_moderator:note1234@sandbox1-wkmdm.mongodb.net/noteDB?retryWrites=true&w=majority";
const client = new MongoClient(uri, { useNewUrlParser: true });

module.exports = class NoteService extends Schmervice.Service {

    async loadAll() {

        let result;

        const connection = await client.connect();
        const db = connection.db('noteDB');
        const collection = db.collection("notes");

        result = await collection.find({}).toArray();
        console.log(result);
        return result;

        // return [
        //     { title: 'bravo' },
        //     { title: 'tango' },
        //     { title: 'bobby' }
        // ]
    }

};
```