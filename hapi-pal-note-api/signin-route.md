# 4. สร้าง Sign in route 

## 1. สร้าง user.signin.js

รันคำสั่ง 

```bash
npx hpal make route default
```

แล้วกำหนด route 

```js
'use strict';

module.exports = {
    method: 'POST',
    path: '/user/signin',
    handler: (request, h) => {
        return { message: 'ok signin' };
    }
}
```