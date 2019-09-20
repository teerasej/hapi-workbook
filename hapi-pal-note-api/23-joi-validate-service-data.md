23. ใช้ joi validate ข้อมูลใน service

เปิดไฟล์ `lib/services/note.js`

```js
'use strict';

const Joi = require('@hapi/joi');

const Schmervice = require('schmervice');
const MongoClient = require('mongodb').MongoClient;
const uri = "...";
const client = new MongoClient(uri, { useNewUrlParser: true });

module.exports = class NoteService extends Schmervice.Service {

    async loadAll() {

        let result;

        const connection = await client.connect();
        const db = connection.db('noteDB');
        const collection = db.collection("notes");

        result = await collection.find({}).toArray();
        console.log(result);
        client.close();
        return result;

    }

    async save(message) {

        // กำหนดค่าด้วย Joi
        const schema = Joi.string().required().min(1);
        // สั่ง validate 
        const { error } = schema.validate(message);
        
        // ถ้ามีค่า error ก็ให้ return ออกไปแทน
        if(error) {
            return { error }
        }

        let result;

        const connection = await client.connect();
        const db = connection.db('noteDB');
        const collection = db.collection("notes");

        result = await collection.insertOne({ title: message });
        client.close();
        return result.ops[0];
    }

};
```