# Day 3 (Deploy)

## API Documents
### [Swagger](https://swagger.io/) 
API Documents แบบ Dynamic 
- สามารถเขียนโค้ดแล้ว Generate API Document 
- สามารถเขียน API Document แล้ว Generate เป็นโค้ดก็ได้

### [API Blueprint](https://apiblueprint.org)
API Blueprint. A powerful high-level API description language for web APIs.
- มี Testing
- มี Mock

## API Gateway
Concept คือมาตรงกลางแล้วแบ่ง request เป็น routes

### [Kong](https://konghq.com/kong/) 
The World’s Most Popular Open Source Microservice API Gateway and Platform.

## Cloud Native
- [Cloud Native Interactive Landscape](https://landscape.cncf.io/)

## DevOps
- ตารางธาตุ https://xebialabs.com/periodic-table-of-devops-tools/

## Service Discovery
- [Consul](https://www.consul.io/)

## Circuit breaker
ทุกภาษาจะมี Library เกี่ยวกับ Circuit breaker ให้อยู่แล้ว
  
### [circuit-breaker.js](https://github.com/yammer/circuit-breaker-js)
- เมื่อมันถูกเปิดขึ้น default มันจะปิดตัวเองภายใน 10วิ

## CQRS
- เกิดจากภาษาเชิง Object Oriented
- แบ่งกลุ่ม services เป็น Query Services (Read) กับ Command Services (Write)
- การแยกกันจะแยกการเก็บ Data ซึ่งพอมี Data หลายที่ มันจึงจำเป็นต้อง Sync กัน โดยให้ `Event Store`
- https://www.rabbitmq.com/

## Event Sourcing
- Immutable
- Time series
- Query ได้
- สามารถย้อนหลัง(Undo) ได้ด้วย
- มี Logs ประวัติข้อมูลทั้งหมด สามารถ Rebuild ทั้งหมดก็จะได้ข้อมูลเดิม
- เลือก Rollback กี่ step ก็ได้
- ทำให้การ Audit ทำได้ง่าย

### [Kafka](https://kafka.apache.org/)
ใช้เป็นตัวกลางในการเชื่อมต่อ เพื่อช่วยแยกการสื่อสารระหว่างระบบแต่ละตัว ไม่ว่าระบบอะไรต้องการข้อมูลจากไหน ก็มาเรียกใช้ใน Apache Kafka ตัวนี้ตัวเดียว
- consume สามารถรันทิ้งไว้หลาย services ได้เลย
- มีการกระจาย (distributed) การเก็บข้อมูลใน clusters
- มีความยืดหยุ่น (resilient architecture) เช่น มีการทำสำเนาข้อมูลซ้ำ (replication)
- มีการทนต่อความเสียหาย (fault tolerent)
- มีความสามารถในการขยายเชิงขนาน หรือ เพิ่มเครื่อง (node) ใน cluster ได้ (horizontal scalability)
- มีประสิทธิภาพด้านความเร็ว (latency น้อยกว่า 10ms)
- มีระบบที่ใหญ่ๆ ที่ใช้ Apache Kafka อยู่มาก เช่น Linkedin, Netflix, AirBnB, Yahoo, Wallmart หรือ LINE สวัสดีวันจันทร์นั่นเองของเรานั่นเองงง

## Notes
- ก่อนเริ่มต้นทำงานเราต้อง Design Contact Point ก่อน
- ยิ่งเป็น Microservices ยิ่งมีเอกสารเยอะ
- หนังสือ Domain-Driven Desing
