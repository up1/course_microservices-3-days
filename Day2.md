# Day 2 (Develop)

- https://grpc.io

### Service Discovery
- มีการ Register Discovery ก่อน แต่ละ Service บอกว่าใช้เครื่องไหนบ้าง
- Service Discovery มีการเช็คผ่าน Health check ว่า Service ยังทำงานปกติอยู่มั้ย?
- ตอน Start และ Shutdown หรือปิด Service จะมีการ Un-register
- Client บอกว่าอยากใช้ service อะไร ก็ไปดูที่ Service register ไว้ ได้ข้อมูลเครื่องที่ Service นั้นๆ Register ไว้
- ทำให้ Load balance จะไปอยู่ฝั่ง Client เพราะ Client เป็นคนเรียน
- กรณีที่ Client มี Request เยอะ ให้ทำ Caching ไว้ที่ฝั่ง Client แต่อาจเกิดปัญหาเครื่องข้อมูลที่ cache ไว้ จะไม่ตรงกัน
- เป็น Syncronuos รูปแบบหนึ่ง

### 12 Factor App
1. ...
9. **Disposability** มีความทนทานถึงขีดสุด ด้วยการ Start ได้อย่างรวดเร็ว และ Shutdown อย่างสง่างาม
> เพิ่มเติม https://12factor.net.
---
## Asynchronous
### Messaging pattern
- ต้องประกอบด้วย ผู้ส่ง -> คนกลาง -> ผู้รับ
- เมื่อมีอะไรที่ต้องจัดลำดับคิว จะมีท่อเพื่อไว้จัดคิว
- จะแบบ Topic หรือ PubSub คือ 1 event จะไปได้หลายที่ *(1)*
- Microservices จะใช้รูปแบบนี้มาก
- แต่ละ Service จะเป็นทั้งผู้ส่ง(Sender) และ ผู้รับ(Receiver)
- ถ้ามี Request เข้ามาเยอะมาก แล้วมีบาง Request ที่พัง ต้องมีตัวช่วยจัดการเพราะมันเป็น un-blocking *(2)* 

> *(1)* เช่นกรณีที่มีการเปลี่ยนข้อมูล Product แล้วทุกๆ Service ที่ใช้ข้อมูล Product เปลี่ยนตามด้วย
> *(2)* เช่น
```
a = 1
b = 1
c = a + b
// c = จะได้ค่าไม่เหมือนเดิมเพราะมันทำงานทุกบรรทัดพร้อมกัน
```
