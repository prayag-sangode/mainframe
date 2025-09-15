# Mainframe Components Table

| **Category**                     | **Component**                             | **Description**                                                   |
| -------------------------------- | ----------------------------------------- | ----------------------------------------------------------------- |
| **Hardware**                     | CPU / CPs                                 | General-purpose processors designed for parallelism & reliability |
|                                  | Memory                                    | High-speed RAM for massive workloads                              |
|                                  | Channels (I/O Processors)                 | Offload I/O from CPU; allow parallel I/O                          |
|                                  | DASD (Storage)                            | Enterprise disk storage (IBM DS8000, etc.)                        |
|                                  | Tape / VTS                                | Backup and archival storage                                       |
|                                  | Networking                                | High-speed network interfaces                                     |
|                                  | Peripherals                               | Terminals (3270), printers, etc.                                  |
| **Processor Types (Engines)**    | CP (Central Processor)                    | General-purpose engine                                            |
|                                  | IFL (Integrated Facility for Linux)       | Runs Linux workloads                                              |
|                                  | zIIP (z Integrated Information Processor) | Optimized for DB2, XML, encryption, analytics                     |
|                                  | zAAP (z Application Assist Processor)     | Java workloads (merged with zIIP later)                           |
|                                  | SAP (System Assist Processor)             | Handles I/O operations                                            |
| **Operating Systems**            | z/OS                                      | Primary enterprise OS                                             |
|                                  | z/VM                                      | Virtualization (hosts multiple OSes)                              |
|                                  | z/VSE                                     | Entry-level OS for business apps                                  |
|                                  | Linux on Z                                | Enterprise Linux on mainframe                                     |
|                                  | z/TPF                                     | High-volume transaction processing (airlines, banking)            |
| **System Software (Subsystems)** | CICS                                      | Online Transaction Processing (OLTP)                              |
|                                  | IMS                                       | Hierarchical DB + transaction management                          |
|                                  | DB2 for z/OS                              | Relational database system                                        |
|                                  | MQ (MQSeries)                             | Messaging & queuing                                               |
| **Security**                     | RACF                                      | Access control & security                                         |
|                                  | ACF2, Top Secret                          | Alternative security products                                     |
| **Middleware**                   | WebSphere, MQ, APIs                       | Integration with modern apps                                      |
| **Application Layer**            | Batch Processing                          | Jobs executed using JCL                                           |
|                                  | Online Processing                         | Real-time transactions (CICS, IMS)                                |
|                                  | Programming Languages                     | COBOL, PL/I, Assembler, Java, REXX, Python                        |
| **Management & Monitoring**      | JES2 / JES3 / SDSF                        | Job scheduling & batch management                                 |
|                                  | SMF / RMF                                 | System & performance monitoring                                   |
|                                  | OMEGAMON                                  | Monitoring & diagnostics                                          |
|                                  | z/OSMF                                    | Web-based management interface                                    |

---

# Mainframe Components vs AWS Equivalents

This is the **high-level migration map**. In practice:

* **COBOL → Java/Python** (via AWS Blu Age refactoring or replatforming).
* **CICS/IMS → Microservices** (API Gateway + Lambda + Aurora/DynamoDB).
* **Batch JCL → AWS Batch / Step Functions / Glue**.
* **DB2 → Aurora / RDS / DynamoDB**.

| **Category**          | **Mainframe Component**              | **Description**                   | **AWS Equivalent (Migration Target)**                                                            |
| --------------------- | ------------------------------------ | --------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Hardware**          | CPU / CPs                            | General-purpose processors        | **EC2 instances** (z/OS emulation needs 3rd-party like Micro Focus, AWS Mainframe Modernization) |
|                       | Memory                               | Large, high-speed RAM             | **EC2 memory-optimized instances** (R7, X7)                                                      |
|                       | Channels (I/O Processors)            | Offload I/O                       | **EBS multi-attach, ENA networking**                                                             |
|                       | DASD (Storage)                       | Enterprise disk storage           | **EBS (block storage), EFS (shared), FSx for NetApp ONTAP**                                      |
|                       | Tape / VTS                           | Backup/archive                    | **S3 Glacier, S3 Glacier Deep Archive**                                                          |
|                       | Networking                           | High-speed comms                  | **VPC, Direct Connect, Transit Gateway**                                                         |
|                       | Peripherals (3270, printers)         | Terminals, printers               | **AWS WorkSpaces, AppStream, Printing via S3/CloudPrint**                                        |
| **Processor Types**   | CP (Central Processor)               | General compute                   | **EC2 compute instances**                                                                        |
|                       | IFL (Linux Facility)                 | Run Linux on mainframe            | **EC2 Linux instances, ECS/EKS containers**                                                      |
|                       | zIIP                                 | DB2, analytics, encryption engine | **Aurora PostgreSQL/ MySQL, DynamoDB, AWS KMS, Glue, Athena**                                    |
|                       | zAAP                                 | Java workloads                    | **Lambda (Java runtime), ECS/EKS with Java apps**                                                |
|                       | SAP                                  | I/O handling                      | **AWS managed storage/networking stack**                                                         |
| **Operating Systems** | z/OS                                 | Enterprise OS                     | **AWS Mainframe Modernization (Blu Age/Micro Focus), EC2 Windows/Linux**                         |
|                       | z/VM                                 | Virtualization                    | **VMware on AWS, EC2 with Nitro Hypervisor**                                                     |
|                       | z/VSE                                | Entry-level OS                    | **EC2 small/medium instances with Linux/Windows**                                                |
|                       | Linux on Z                           | Enterprise Linux                  | **EC2 Linux, ECS/EKS, Fargate**                                                                  |
|                       | z/TPF                                | Airline/high-volume TP            | **Aurora + Lambda + API Gateway (event-driven microservices)**                                   |
| **Subsystems**        | CICS                                 | Transaction processing            | **Amazon MQ, API Gateway + Lambda, Step Functions**                                              |
|                       | IMS                                  | Hierarchical DB + TP              | **DynamoDB (NoSQL), Aurora (SQL), Step Functions**                                               |
|                       | DB2 for z/OS                         | RDBMS                             | **Amazon Aurora (PostgreSQL/MySQL), RDS DB2 (via partner)**                                      |
|                       | MQ (MQSeries)                        | Messaging                         | **Amazon MQ, SQS, SNS, EventBridge**                                                             |
| **Security**          | RACF / ACF2 / Top Secret             | Identity & access mgmt            | **IAM, AWS Organizations, KMS, Secrets Manager**                                                 |
| **Middleware**        | WebSphere, MQ, APIs                  | App servers + messaging           | **Amazon MQ, AWS App Runner, ECS/EKS + Spring Boot/Java**                                        |
| **Applications**      | Batch Processing (JCL)               | Job scheduling                    | **AWS Batch, Step Functions, Glue ETL, Lambda**                                                  |
|                       | Online Processing                    | Real-time OLTP                    | **API Gateway + Lambda + Aurora/DynamoDB**                                                       |
|                       | Programming (COBOL, PL/I, Assembler) | App dev stack                     | **AWS Mainframe Modernization (Blu Age for COBOL→Java), Java/Python on ECS/EKS/Lambda**          |
| **Management**        | JES2/JES3                            | Job scheduling                    | **AWS Batch, Step Functions, Data Pipeline**                                                     |
|                       | SMF/RMF                              | Monitoring & logs                 | **CloudWatch, CloudTrail, X-Ray**                                                                |
|                       | OMEGAMON                             | Perf monitoring                   | **CloudWatch, AWS Managed Grafana, Prometheus**                                                  |
|                       | z/OSMF                               | Web mgmt console                  | **AWS Console, AWS Systems Manager**                                                             |

---


