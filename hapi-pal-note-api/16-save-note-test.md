# 16. สร้าง test unit สำหรับ save note

สร้างไฟล์​ `test/note-save.test.js`

```js
const Lab = require('@hapi/lab');
const { expect } = require('@hapi/code');
const Server = require('../server');
const sinon = require('sinon');

const NoteService = require('../lib/services/note');

describe('Note Save Operation', () => {

    let server;
    let stubNoteSave;

    beforeEach(async () => {
        server = await Server.deployment(false);
        stubNoteSave = sinon.stub(NoteService.prototype, 'save');
    });

    afterEach(async () => {
        sinon.restore();
        await server.stop();
    });


    it('Save successful', async () => {

        const inputPayload = {
            message: 'Nextflow'
        }

        const successPayload = {
            _id: 1,
            title: 'Nextflow'
        }

        stubNoteSave.onFirstCall().returns(successPayload);

        const result = await server.inject({
            method:'post',
            url:'/notes',
            payload: inputPayload
        });

        expect(result.statusCode).to.equal(200);

        const resultJSON = JSON.parse(result.payload);
        expect(resultJSON).to.exist();
        expect(resultJSON._id).to.exist();
        expect(resultJSON.title).to.exist();
        expect(resultJSON.title).to.equal(successPayload.title);
    });

}); 
```