# 2. Configuration-oriented Project

- Hapi สร้างขึ้นโดยแนวคิดการ configuration โดยเฉพาะ
- `libs/` จะเป็นที่เก็บโค้ดส่วน business logic ต่างๆ เช่น Route, Service, Helper
- `server/` จะเป็นที่เก็บ configuration ต่างๆ 

## 1. ส่วน configuration 

### A. ไฟล์ `server/.env`

ปกติ Hapi จะมีไฟล์ `server/.env-keep` มาให้ ให้เรา duplicate ไฟล์นี้ เป็นอีกไฟล์ที่ชื่อ `.env` เพื่อให้ server เราสามารถโหลดค่าไปใช้งานได้ 

ตอนนี้เราจะเขียนแค่ด้านล่างลงไปใน `server/.env` ก่อน

```
NODE_ENV=development
```

#### สำคัญ

- **ไฟล์นี้จะไม่เอาขึ้น git repo นะ นะ นะ** (`.gitignore` เขียนไว้แล้วไม่ต้องห่วง)
- เวลาเขียนอะไรลงไปใน `.env` ก็อย่าลืมเอาค่านั้นมาเขียนเป็น guideline ในไฟล์​ `.env-keep` ด้วย คนอื่นที่เอาโปรเจคเราไป จะได้รู้ว่าต้องกำหนดค่าอะไรบ้าง


### B. ไฟล์ `server/manifest.js`

จะเป็นส่วนที่ configure ค่าต่างๆ สำหรับ server ของเรา เช่น

- การโหลดค่า จากไฟล์​ `.env` 
- หมายเลข port 

```js
'use strict';

const Dotenv = require('dotenv');
const Confidence = require('confidence');
const Toys = require('toys');

// Pull .env into process.env
Dotenv.config({ path: `${__dirname}/.env` });

// Glue manifest as a confidence store
module.exports = new Confidence.Store({
    server: {
        host: 'localhost',
        port: {
            $env: 'PORT',
            $coerce: 'number',
            $default: 3000
        },
        debug: {
            $filter: { $env: 'NODE_ENV' },
            $default: {
                log: ['error'],
                request: ['error']
            },
            production: {
                request: ['implementation']
            }
        }
    },
    register: {
        plugins: [
            {
                plugin: '../lib', // Main plugin
                options: {}
            },
            {
                plugin: {
                    $filter: { $env: 'NODE_ENV' },
                    $default: 'hpal-debug',
                    production: Toys.noop
                }
            }
        ]
    }
});

```