# Day 2 (Develop)

### Service Discovery
- มีการ Register Discovery ก่อน แต่ละ Service บอกว่าใช้เครื่องไหนบ้าง
- Service Discovery มีการเช็คผ่าน Health check ว่า Service ยังทำงานปกติอยู่มั้ย?
- ตอน Start และ Shutdown หรือปิด Service จะมีการ Un-register
- Client บอกว่าอยากใช้ service อะไร ก็ไปดูที่ Service register ไว้ ได้ข้อมูลเครื่องที่ Service นั้นๆ Register ไว้
- ทำให้ Load balance จะไปอยู่ฝั่ง Client เพราะ Client เป็นคนเรียน
- กรณีที่ Client มี Request เยอะ ให้ทำ Caching ไว้ที่ฝั่ง Client แต่อาจเกิดปัญหาเครื่องข้อมูลที่ cache ไว้ จะไม่ตรงกัน
- เป็น Syncronuos รูปแบบหนึ่ง

### 12 Factor App
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
- ถ้ามี Request เข้ามาเยอะมาก แล้วมีบาง Request ที่พัง ต้องมีตัวช่วยจัดการเพราะมันเป็น un-blocking
```javascript
a = 1
b = 1
c = a + b
// c = จะได้ค่าไม่เหมือนเดิมเพราะมันทำงานทุกบรรทัดพร้อมกัน
```

### Drawbacks (ข้อเสีย)
- อาจมีปัญหาคอขวด
- มีความซับซ้อนสูง
- Single point of failure

### CAP Theorem
- คือ Consistency, Availability, Partition Tolerance
- ข้อแม้คือเลือกได้แค่ 2 ใน 3 อย่าง
- RDMS ใช้แค่ Consistency กับ Availability
- ถ้าเลือก C, P ระบบต้อง Sync กัน
- ฝากเช็คธนาคารทำไมไม่ Consistency? เพราะใช้ Cron Job รันตอนเที่ยง ทำให้ฝากวันนี้หลังบ่ายอาจได้พรุ่งนี้
- ในโลกของระบบแบบ Distributed จะอ้างอิงถึง CAP Theorem

### Event-based communication
- Message กับ Event ต่างกันอย่างไร? `Message` จะระบุผู้รับชัดเจน ส่วน `Event` ไม่ระบุปลายทาง มีหน้าที่แค่ Boardcast ข้อมูลอย่างเดียว
- 1 Message อาจทำให้เกิดได้หลาย Events

## Synchronous process
- Client Service(ผู้เรียก) จะ Asynchronous ส่วน Services(ดำเนินการ) จะเป็นแบบ Synchronous

## Consistency patterns
- Compensating active (Undo)
- Retry ลองใหม่ไปเรื่อยๆ จนกว่าจะ Timeout
- Ignore ไม่ต้องไปสนใจ
- Restart เริ่มทำตั้งแต่ต้นใหม่
- Tentative operation (เดี๋ยวค่อยมา Adjust กันใหม่)

## Event sourcing
- นึกภาพถึง Blockchain คือการเรียก Event เป็น blocks เรียงกันไปเป็น chain
- ลำดับของ events จะเก็บไว้ที่ `Event store`
- Can decouple services (query and command)

## CRUD -> CQRS (การแยกการทำงานตาม Operation)
แยกเป็น `Read Service` กับ `Write Service` เพื่อไม่ใช้เกิด Deadlock เมื่อ DB ก้อนเดียวมีการ R/W พร้อมกันเป็นจำนวนมาก
- C,U,D เรียกใหม่เป็น command
- R เรียนใหม่เป็น Query 

## Query data from multiple services
- API composition
- Cold cata from services
- CQRS (Command Query Responsibility Segregation)

## NoSQL
- Document
- Key-Value
- Column base
- Graph

## Integrate services with Uer Interface
- ใช้ `BFF` (Backend For Frontend)
- ใช้ Microfrontend
- แต่ละทีมทำตั้งแต่ Frontend ยัน Backend (แต่ทุกทีมทำ Product เดียวกันนะ)

### Zipkin
- ทำเรื่อง tracing system
- ต้องไป enable ในแต่ละ service state
- https://zipkin.apache.org/

### Tracing
- แต่ละ Request สมมติว่าใช้เวลา 10วิ เรียกเป็น 1 Trace
- ในแต่ละ Trace มีหลายขั้นตอน แต่ละขั้นตอนเรียกว่า SPAN
- เชื่อมโยงกันโดยใช้ Tracing ID

### Microservice 1.0
- `Configuration` ใช้ Config Server (Spring Cloud Config Server)
- `Service Discovery`
- `Fault Tolerance`
- `Tracing and Visibility`

## Other notes
- อะไรก็ตามที่ขึ้นต้นว่า General แม่งหน้ากลัวมาก (Purpose มันไม่ชัดเจน)
- เมื่อเจอปัญหาเราควรแก้ที่ปัญหาที่แท้จริง ไม่ใช่แค่ Work Around
- Line App ใช้ Kafka เป็นตัวส่ง Message ทั้งหมด
- อันดับ DBMS ที่นิยมมากที่สุด https://db-engines.com/en/ranking
- https://grpc.io

> *(1)* เช่นกรณีที่มีการเปลี่ยนข้อมูล Product แล้วทุกๆ Service ที่ใช้ข้อมูล Product เปลี่ยนตามด้วย
