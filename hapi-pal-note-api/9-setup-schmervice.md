# 9. ติดตั้ง และตั้งค่า Service (schemervice)

## 1. ติดตั้ง module 

```bash
npm install schmervice
```

หรือ 

```bash
yarn add schmervice
```

## 2. เพิ่ม plugin options ของ schmervice เข้าไปในโปรเจค

ใช้คำสั่ง `npx hpal make plugin schmervice` เพื่อสร้างไฟล์นี้ และ haute-couture จะได้อ่านเข้าไปในระบบ

เปิดไฟล์ `lib/plugins/schmervice.js`

```js
'use strict';

module.exports = {
};
```