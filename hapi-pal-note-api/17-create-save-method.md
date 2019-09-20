
# 17. สร้าง save method ใน Note Service 

เปิดไฟล์ `lib/services/note.js`

และเพิ่ม method `save(message)` ลงไป

```js
 async save(message) {

        let result;

        const connection = await client.connect();
        const db = connection.db('noteDB');
        const collection = db.collection("notes");

        result = await collection.insertOne({ title: message });
        console.log(result);
        return result;
    }
```

## 2. อย่าลืมปิด connection ด้วยล่ะ 

```js
async loadAll() {

        let result;

        const connection = await client.connect();
        const db = connection.db('noteDB');
        const collection = db.collection("notes");

        result = await collection.find({}).toArray();
        console.log(result);

        // ปิดการเชื่อมต่อ
        client.close();

        return result;

    }

    async save(message) {
        
        let result;

        const connection = await client.connect();
        const db = connection.db('noteDB');
        const collection = db.collection("notes");

        result = await collection.insertOne({ title: message });
        console.log(result);

        // ปิดการเชื่อมต่อ
        client.close();

        return result;
    }
```