# 13. ปรับการ test

ตอนนี้จะเห็นว่าการรันเทสใช้เวลานานขึ้นจน Jest timeout 
เราสามารถกำหนดค่า timeout ให้ jest ได้ 

```js
it('GET All existed', async () => {

        jest.setTimeout(30000);
        // ...

}

it('Got a load of notes', async () => {

        jest.setTimeout(30000);
        // ...

}
```

## ไฟล์เต็ม `test/get-all.test.js`

```js
const Lab = require('@hapi/lab');
const { expect } = require('@hapi/code');
const Server = require('../server');

describe('Note route', () => {
    
    let server;

    beforeEach(async () => {
        server = await Server.deployment(false);
    });

    afterEach(async () => {
        await server.stop();
    });


    it('GET All existed', async () => {

        jest.setTimeout(30000);

        const result = await server.inject({
            method:'get',
            url:'/notes'
        });

        expect(result.statusCode).to.equal(200);
    });

    it('Got a load of notes', async () => {

        jest.setTimeout(30000);

        const result = await server.inject({
            method:'get',
            url:'/notes'
        });

        const resultJSON = JSON.parse(result.payload);
        expect(resultJSON).to.be.an.array();
    });

});
```