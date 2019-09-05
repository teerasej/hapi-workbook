

# 2. First Web API 

## 1. สร้าง Route ของ API แรก

สร้างไฟล์ `index.js`

เราจะสร้างส่วนที่จะรัน server ด้วย Hapi module ขึ้นมา 

```js
`use strict`;
const Hapi = require('@hapi/hapi');

const init = async () => {

    
};

process.on('unhandledRejection', (err) => {
    console.log(err);
    process.exit(1);
});

init(); 
```

ในส่วนของ function `init` เราจะ สั่งรัน server ที่ `localhost:3000`

```js
const init = async () => {

    const server = Hapi.server({
        port: 3000,
        host: 'localhost'
    });



    await server.start();
    console.log('Server running on %s', server.info.uri);
};

```
 

## ไฟล์เต็ม `index.js`

```js
`use strict`;
const Hapi = require('@hapi/hapi');

const init = async () => {

    const server = Hapi.server({
        port: 3000,
        host: 'localhost'
    });



    await server.start();
    console.log('Server running on %s', server.info.uri);
};

process.on('unhandledRejection', (err) => {

    console.log(err);
    process.exit(1);
});

init(); 
```

