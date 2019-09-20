# 7. ติดตั้ง และตั้งค่า jest 

## 1. รันคำสั่งติดตั้ง 

```bash
npm install jest 
```

หรือ

```bash
yarn add jest --dev
```

## 2. ตั้งค่า test script 

เปิดไฟล์​ `package.json` และแก้ไขค่า Scripts > Test ไปใช้ jest แทน

```json
"scripts": {
    "start": "node server",
    "test": "jest --watchAll",  // แก้ตรงนี้
    "lint": "eslint ."
  },
```