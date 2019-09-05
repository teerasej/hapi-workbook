
# Setup 

## 1. สร้างโฟลเดอร์โปรเจค

```bash
mkdir my-web-api

// รันคำสั่งเพื่อสร้าง package.json แล้วกรอกข้อมูล package ตามปกติ
npm init 
```

## 2. ติดตั้ง hapi

```bash
cd my-web-api

yarn add @hapi/hapi
yarn add @hapi/lab --dev
yarn add @hapi/code --dev
yarn add hpal --dev
```


## 3. ติดตั้งเครื่องมืออื่นๆ 

### 1. PM2 ช่วยในการ dev

```bash
yarn global add pm2
```

### 2. VSCode Extension

1. [Hapi Snippet](https://marketplace.visualstudio.com/items?itemName=deerawan.vscode-hapijs-snippets)
2. [gitignore](https://marketplace.visualstudio.com/items?itemName=codezombiech.gitignore)