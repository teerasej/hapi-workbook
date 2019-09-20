
# 1. สร้างโปรเจค 

## 1. สร้างโปรเจคด้วย hpal

เปิด Terminal และรันคำสั่ง 

```bash
npx hpal new nextflow-note-api
```

## 2. ติดตั้ง module 

```bash
cd nextflow-note-api
npm install
```
หรือ
```bash
cd nextflow-note-api
yarn install
```

## 3. ทดสอบรันโปรเจค

```bash
npm start
```
หรือ
```bash
yarn start
```

แล้วทดสอบยิง request ไปที่ `0.0.0.0:3000` ด้วยคำสั่ง 

```bash
curl http://0.0.0.0:3000
```

น่าจะได้ผลลัพธ์

```json
{
  "statusCode": 404,
  "error": "Not Found",
  "message": "Not Found"
}
```