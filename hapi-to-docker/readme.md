
# Hapi to Docker

## 1. Setup 

1. ถ้ายังไม่มี ก็โหลดและติดตั้ง [Docker Desktop](https://www.docker.com/products/docker-desktop)
2. [VSCode Extension: Docker by Microsoft](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)

## 2. สร้าง Docker Image ด้วย Dockerfile

สร้างไฟล์ชื่อ `Dockerfile` เป็น Script สำหรับการสร้าง Image  

และเขียน script 

```dockerfile
FROM node:10.16.3-jessie-slim

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY package.json /usr/src/app/
RUN npm install

COPY . /usr/src/app

EXPOSE 3000

CMD ["npm","start"]
```

1. สังเกตว่าเราใช้ node:boron ที่จะดึง Node.js เวอร์ชั่น LTS มาใช้งานใน Docker Image ของเรา สั่งสร้างโฟลเดอร์​ และกำหนดเป็น Working Directory
2. ก๊อปปี้ไฟล์ package.json ไปไว้ในโฟลเดอร์ /usr/src/app/ 
3. ก่อนที่จะสั่งติดตั้ง Node module ด้วยคำสั่ง npm install
4. ก๊อปปี้ไฟล์ที่เหลือไปไหว้ในโฟลเดอร์ดังกล่าว
5. เปิด Port 3000
6. สั่งรัน npm start เพื่อเริ่มการทำงานของ  Web Server

## ละเว้นไฟล์และโฟลเดอร์จาก Docker ด้วย `.dockerignore`

สร้างไฟล์ `.dockerignore`

เขียนรายการลงไปในไฟล์ 

```
node_modules
npm-debug.log
```

## สร้างไฟล์ docker 

1. คลิกขวาที่ไฟล์ **Dockerfile**
2. เลือกคำสั่ง **build image...**
3. กำหนด tag เช่น `hapi-note-swagger-nextflow:latest`
4. รอการดาวน์โหลดจนเสร็จสมบูรณ์

## รัน Docker image

1. เปิดไปที่ Tab Docker
2. Image > ชื่อ Image > คลิกขวาที่ชื่อ Tag 
3. เลือกคำสั่ง Run Interactively