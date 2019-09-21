# 5. กำหนดค่า module **HauteCouture** 
   
กำหนดการตั้งค่า [HauteCouture](https://github.com/hapipal/haute-couture) ให้อ่านไฟล์ใน subfolder ด้านใน routes ได้ มีประโยชน์ต่อการจัดการไฟล์ route และส่วนประกอบอื่นๆ 

เช่นปกติเราจะทำได้แค่: `lib/routes/nextflow.js` 

แต่ปรับแล้วเราจะทำโครงสร้างแบบนี้ได้: `lib/routes/company/nextflow.js` 

```js
// lib/.hc.js

'use strict';

module.exports = {
    recursive: true
}; 
```
