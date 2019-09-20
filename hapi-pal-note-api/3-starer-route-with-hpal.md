# 3. สร้าง Starter Route ด้วย Hapi Pal

## 1. ติดตั้ง module `hpal`

```bash
npm install --save-dev hpal
```

หรือ 

```bash
yarn add hpal --dev
```

## 2. รันคำสั่ง generate route 

รันคำสั่ง 

```bash
npx hpal make route default
```

จะได้ไฟล์ `lib/routes/default.js` ที่มีโค้ดแบบด้านล่าง 

```js
'use strict';

module.exports = {
    method: '',
    path: '',
    options: {
        handler: async (request, h) => {}
    }
};
```

กำหนดค่าลงไปดังนี้ 

```js
'use strict';

module.exports = {
    method: 'GET',
    path: '/',
    options: {
        handler: async (request, h) => {
            return { message: 'oh hello!' }
        }
    }
}
```

## 3. ทดสอบ

restart server ใหม่ และทดสอบยิง request เข้าไปที่ `localhost:3000`