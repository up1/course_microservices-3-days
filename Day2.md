# Day 2

- https://grpc.io

### Service Discovery
- มีการ Register Discovery ก่อน แต่ละ Service บอกว่าใช้เครื่องไหนบ้าง
- Service Discovery มีการเช็คผ่าน Health check ว่า Service ยังทำงานปกติอยู่มั้ย?
- ตอน Start และ Shutdown หรือปิด Service จะมีการ Un-register
- Client บอกว่าอยากใช้ service อะไร ก็ไปดูที่ Service register ไว้ ได้ข้อมูลเครื่องที่ Service นั้นๆ Register ไว้
- ทำให้ Load balance จะไปอยู่ฝั่ง Client เพราะ Client เป็นคนเรียน
- กรณีที่ Client มี Request เยอะ ให้ทำ Caching ไว้ที่ฝั่ง Client แต่อาจเกิดปัญหาเครื่องข้อมูลที่ cache ไว้ จะไม่ตรงกัน
- เป็น Syncronuos รูปแบบหนึ่ง

### 12 Factor App [^1]
1. dd
9. **Disposability** มีความทนทานถึงขีดสุด ด้วยการ Start ได้อย่างรวดเร็ว และ Shutdown อย่างสง่างาม
Here's a sentence with a footnote. [^1]

[^1]: This is the footnote.
[^2]: เพิ่มเติม. https://12factor.net
