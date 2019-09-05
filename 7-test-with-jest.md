
# 7. ทดลอง test ด้วย Jest 

## 1. รันคำสั่งติดตั้ง jest

```bash
yarn add jest --dev
```

## 2. ปรับไฟล์​ package.json 

แก้ไขในส่วน script 

```json
"scripts": {
    "test": "jest --watchAll --coverage"
},
```

## 3. ไม่จำเป็นต้อง import จาก jest

สร้างไฟล์ `test/authen.signin.test.js` 

เราสามารถ comment ส่วนที่ import ของ lab ในไฟล์ `test/example.test.js` ได้ดังนี้ 

```js
const Lab = require('@hapi/lab');
const { expect } = require('@hapi/code');
// const { afterEach, beforeEach, describe, it } = exports.lab = Lab.script();
const { init } = require('../lib/server');
```

## 4. เขียน test group สำหรับ Sign In route 

```js
describe('Authenticate - Sign In', () => {

    let server;

    beforeEach(async () => {
        server = await init();
    });

    afterEach(async () => {
        await server.stop();
    });

    it('should return 404', async () => {

        let options = {
            url: '/blahblah',
            method: 'POST'
        }

        const response = await server.inject(options);
        expect(response.statusCode).to.equal(404);

    });

    it('should pass authentication', async () => {

        const payload = { username: 'a', password: 'pass' };

        options = {
            url: '/user/signin',
            method: 'POST',
            payload: payload
        }

        const response = await server.inject(options);

        expect(response.statusCode).to.equal(200);

        const resultJSON = JSON.parse(response.payload)
        expect(resultJSON.token).to.exist();
        expect(resultJSON.token).to.equal('123456');

    });

}); 
```

## 5. สร้าง route signin

สร้างไฟล์ `lib/routes/user.signin.route.js`

```js
module.exports = {
    method: 'POST',
    path: '/user/signin',
    handler: () => {
        return { token: '123456' };
    }
  }
```

## 6. โหลด route Sign In ใส่ server

เปิดไฟล์ `lib/server.js`

```js
const routeUserSignIn = require('./routes/user.signin.route')

server.route(routeUserSignIn)
```

## ไฟล์เต็ม `lib/server.js`

```js
const Hapi = require('@hapi/hapi');
const routeUserSignIn = require('./routes/user.signin.route')

const server = Hapi.server({
    port: 3000,
    host: 'localhost'
});

server.route({
  method: 'GET',
  path: '/',
  handler: function () {

      return 'Hello World!';
  }
});

server.route(routeUserSignIn)

exports.init = async () => {

    await server.initialize();
    return server;
};

exports.start = async () => {

    await server.start();
    console.log(`Server running at: ${server.info.uri}`);
    return server;
};

process.on('unhandledRejection', (err) => {

    console.log(err);
    process.exit(1);
});
```