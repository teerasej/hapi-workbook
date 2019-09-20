# 21. เขียน test ให้ NoteService.save()

สร้างไฟล์ `test/note.test.js`

```js
const Lab = require('@hapi/lab');
const { expect } = require('@hapi/code');

const NoteService = require('../lib/services/note');


describe('Note Service', () => {

    it('test Save Note', async () => {

        const mockMessage = 'test';

        const service = new NoteService();
        let result = await service.save(mockMessage);

        expect(result.title).to.equal(mockMessage);
        expect(result._id).to.exist();
    });

}); 
```

ผลการเทสจะพบว่าต้องมาแก้ใน `save()` ให้ return ค่านี้ออกไปแทน (ดูที่มาได้จาก [Node MongoDB](http://mongodb.github.io/node-mongodb-native/3.1/api/Collection.html#~insertOneWriteOpResult))

เปิดไฟล์ `lib/services/note.js`

```js
async save(message) {
        
        let result;

        const connection = await client.connect();
        const db = connection.db('noteDB');
        const collection = db.collection("notes");

        result = await collection.insertOne({ title: message });
        client.close();
        return result.ops[0];
    }

```