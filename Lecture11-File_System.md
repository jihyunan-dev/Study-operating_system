## Lecture11. File System

---

> ### Outline
>
> - Disk System
> - File System
> - Directory Structure
> - File Protection
> - Allocation Methods
> - Free Space Management

---

### ๐ Disk System

#### ๐**Disk pack**

- ๋ฐ์ดํฐ ์๊ตฌ ์ ์ฅ ์ฅ์น (๋นํ๋ฐ์ฑ)
- ๊ตฌ์ฑ

  - Sector : ๋ฐ์ดํฐ ์ ์ฅ/ํ๋์ ๋ฌผ๋ฆฌ์  ๋จ์
  - Track : Platter ํ ๋ฉด์์ ์ค์ฌ์ผ๋ก ๊ฐ์ ๊ฑฐ๋ฆฌ์ ์๋ sector๋ค์ ์งํฉ
  - Cylinder : ๊ฐ์ ๋ฐ์ง๋ฆ์ ๊ฐ๋ track์ ์งํฉ
  - Platter  
    โ ์๋ฉด์ ์์ฑ ๋ฌผ์ง์ ์ํ ์ํ ๊ธ์ํ  
    โ ๋ฐ์ดํฐ์ ๊ธฐ๋ก/ํ๋์ด ๊ฐ๋ฅํ ๊ธฐ๋ก ๋งค์ฒด
  - Surface : Platter์ ์๋ฉด๊ณผ ์๋ซ๋ฉด

  <img src="https://blog.kakaocdn.net/dn/50daA/btqPYTxKDF8/3xXx6DqlwfeyUDQ93JMKCk/img.png" width="450px">

#### ๐**Disk drive**

- Disk pack์ ๋ฐ์ดํฐ๋ฅผ ๊ธฐ๋กํ๊ฑฐ๋ ํ๋ํ  ์ ์๋๋ก ๊ตฌ์ฑ๋ ์ฅ์น
- ๊ตฌ์ฑ

  - Head : ๋์คํฌ ํ๋ฉด์ ๋ฐ์ดํฐ๋ฅผ ๊ธฐ๋ก/ํ๋
  - Arm : Head๋ฅผ ๊ณ ์ /์งํฑ
  - Positioner (boom) : Arm์ ์งํฑ, Head๋ฅผ ์ํ๋ track์ผ๋ก ์ด๋
  - Spidle : Disk pack์ ๊ณ ์  (ํ์ ์ถ), ๋ถ๋น ํ์  ์ (RPM, Revolutions Per Minute)

  <img src="https://user-images.githubusercontent.com/37871541/78574512-0d656400-7865-11ea-9b48-ccb8e23b1d65.png" width="450px">

#### ๐**Disk Address**

1. Physical disk address  
   โ Sector (๋ฌผ๋ฆฌ์  ๋ฐ์ดํฐ ์ ์ก ๋จ์)๋ฅผ ์ง์   
   โ Cylinder Number | Surface Number | Sector Number ์ด๋ฐ ์์ผ๋ก ๋ฌผ๋ฆฌ์  ์ฃผ์ ์ง์ 

2. Logical disk address: relative address  
   โ Disk system์ ๋ฐ์ดํฐ ์ ์ฒด๋ฅผ *block๋ค์ ๋์ด*๋ก ์ทจ๊ธ  
    ( Bโ | Bโ | Bโ | Bโ | <- ์ด๋ฐ ์์ผ๋ก)
   - Block์ ๋ฒํธ ๋ถ์ฌ
   - ์์์ block์ ์ ๊ทผ ๊ฐ๋ฅ  
     โ Block ๋ฒํธ โ physical address ๋ชจ๋ ํ์ (disk driver)

- Disk Address Mapping  
  : OS ์์ฅ์์ Disk๋ Block๋ค์ ์งํฉ์ด๋ฏ๋ก, Disk์ ์ ๊ทผํ  ๋ Block ๋ฒํธ๋ฅผ ์ ๋ฌ โ Disk driver์์ Physical address๋ก ๋ณํํด์ Disk controller์ ์ ๊ทผ

#### ๐**Data Access in Disk System**

1. Seek time  
   : ๋์คํฌ head๋ฅผ ํ์ํ cylinder๋ก ์ด๋ํ๋ ์๊ฐ
2. Rotational delay  
   : 1๋ฒ ์ดํ๋ถํฐ, ํ์ํ sector๊ฐ ํ์ํ head ์์น๋ก ๋์ฐฉํ๋ ์๊ฐ
3. Data transmission time  
   : 2๋ฒ ์ดํ๋ถํฐ, ํด๋น sector๋ฅผ ์ฝ์ด์ ์ ์ก(or ๊ธฐ๋ก)ํ๋ ์๊ฐ

- 1~3๋ฒ ์๊ฐ์ ๋ชจ๋ ๋ํ ๊ฒ์ data access time์ด๋ผ๊ณ  ํ๋ค!โจโจ

### ๐File System

: ์ฌ์ฉ์๋ค์ด ์ฌ์ฉํ๋ ํ์ผ์ ๊ด๋ฆฌํ๋ ์ด์์ฒด์ ์ ํ ๋ถ๋ถ

- ํ์ผ์์คํ์ ๊ตฌ์ฑํ๋ ์์
  - Files : ์ฐ๊ด๋ ์ ๋ณด์ ์งํฉ
  - Directory structure : ์์คํ ๋ด ํ์ผ๋ค์ ์ ๋ณด๋ฅผ ๊ตฌ์ฑ ๋ฐ ์ ๊ณต
  - Partitions : Directory๋ค์ ์งํฉ์ ๋ผ๋ฆฌ์ /๋ฌผ๋ฆฌ์ ์ผ๋ก ๊ตฌ๋ถ

### ๐ 1. **File** Concept

- **๋ณด์กฐ ๊ธฐ์ต ์ฅ์น์ ์ ์ฅ๋ ์ฐ๊ด๋ ์ ๋ณด๋ค์ ์งํฉ**
  - ๋ณด์กฐ ๊ธฐ์ต ์ฅ์น ํ ๋น์ _์ต์ ๋จ์_
  - Sequence of bytes (๋ฌผ๋ฆฌ์  ์ ์)
- ๋ด์ฉ์ ๋ฐ๋ฅธ ๋ถ๋ฅ
  - Program file : source program / object program, executable files
  - Data file
- ํํ์ ๋ฐ๋ฅธ ๋ถ๋ฅ
  - Text (ascii) file
  - Binary file (0๊ณผ 1๋ก ๊ตฌ์ฑ๋ ํ์ผ)
- File attributes (์์ฑ)  
  : name, identifier, type, location, size, protection ๋ฑ
- File operation  
  : Create, Write, Read, Reposition, Delete, Etc.
- โจโจ **OS**๋ file operation๋ค์ ๋ํ **system call**์ ์ ๊ณตํด์ผ ํจ

#### ๐**File Access Methods**

- Sequential access (์์ฐจ ์ ๊ทผ)  
  : File์ record(or bytes) ๋จ์๋ก ์์๋๋ก ์ ๊ทผ
- Directed access (์ง์  ์ ๊ทผ)  
  : ์ํ๋ block์ ์ง์  ์ ๊ทผ
- Indexed access  
  : Index๋ฅผ ์ฐธ์กฐํ์ฌ ์ํ๋ block์ ์ฐพ์ ํ ๋ฐ์ดํฐ์ ์ ๊ทผ

#### ๐**Directory**

- File๋ค์ *๋ถ๋ฅ, ๋ณด๊ด*ํ๊ธฐ ์ํ ๊ฐ๋
- Operations on directory  
  : Search, Create, Delete, List a Directroy, Rename, Traverse the file system

#### ๐**Partitions**(minidisk, volumes)

- Virtual disk

#### ๐(์ฉ์ด) Mounting

: ํ์ฌ FS์ ๋ค๋ฅธ FS๋ฅผ ๋ถ์ด๋ ๊ฒ  
 (์๋๋ก์ด๋์์ SD์นด๋๋ฅผ ๋ฃ๊ณ  ๋บ ๋ ๋ง์ดํ ์ด์ผ๊ธฐ๊ฐ ๋์ค๊ธฐ๋ ํจ)

### ๐Directory Structure

#### ๐**Flat Directory Structure**

- FS ๋ด์ ํ๋์ directory๋ง ์กด์ฌ(์ต์ด์ mp3๋๋)
- Issues

  - File naming
  - File protection
  - File management

  โป ๋ค์ค ์ฌ์ฉ์ ํ๊ฒฝ์์ ๋ฌธ์ ๊ฐ ๋์ฑ ์ปค์ง

#### ๐**2-Level Directory Structure**

- ์ฌ์ฉ์๋ง๋ค ํ๋์ directory ๋ฐฐ์ 
- ๊ตฌ์กฐ
  - MFD (Master File Directory)
  - UFD (User File Directory)
- Problems
  - Sub-directory ์์ฑ ๋ถ๊ฐ๋ฅ \_ ์ฌ์ ํ file naming ๋ฌธ์ ๊ฐ ๋จ์
  - ์ฌ์ฉ์๊ฐ ํ์ผ ๊ณต์  ๋ถ๊ฐ

#### ๐**Hierarchical Directory Structure**

- Tree ํํ์ ๊ณ์ธต์  directory ์ฌ์ฉ ๊ฐ๋ฅ
- ์ฌ์ฉ์๊ฐ ํ๋ถ directory ์์ฑ/๊ด๋ฆฌ ๊ธฐ๋ฅ
  - System call(OS)์ด ์ ๊ณต๋์ด์ผ ํจ
  - Terminologies
    - Home directory(root), Current directory
    - Absolute pathname(์ ๋๊ฒฝ๋ก: home๋ถํฐ ๋ชฉํ๊น์ง ์ ๋ ๊ฒ), Relative pathname(์๋๊ฒฝ๋ก: current directory๊ธฐ์ค )
- ๋๋ถ๋ถ์ OS๊ฐ ์ฌ์ฉโญ

#### ๐**Acyclic Graph Directory Structure**(๋ฃจํ๊ฐ ๋ง๋ค์ด์ง์ง๋ ์์)

- hierachical directory structure ํ์ฅ
- Directory์์ shard directory, shared file๋ฅผ ๋ด์ ์ ์์
- **Link**์ ๊ฐ๋ ์ฌ์ฉ(์ฝ๊ฐ windows์ ๋ฐ๋ก๊ฐ๊ธฐ ๋๋)

#### ๐**General Graph Directory Structure)**(๋ฃจํ ๊ฐ๋ฅ)

- Acyclic Graph Directory Structure์ ์ผ๋ฐํ
- ๐น๋ฌดํ loop ๋ฐ์ํ  ์ ์์

### ๐File Protection

: File์ ๋ํ ๋ถ์ ์ ํ ์ ๊ทผ ๋ฐฉ์ง โ ๋ค์ค ์ฌ์ฉ์ ์์คํ์์ ๋์ฑ ํ์!

- ์ ๊ทผ ์ ์ด๊ฐ ํ์ํ ์ฐ์ฐ๋ค

  - Read (R)
  - Write (W)
  - Execute (X)
  - Append (A)

- ๐**File Protection Mechanism**  
  โ  Password ๊ธฐ๋ฒ

  - ๊ฐ file๋ค์ PW๋ถ์ฌ
  - ๋นํ์ค์   
    โ ์ฌ์ฉ์๋ค์ด ๋ชจ๋  ๋น๋ฐ๋ฒํธ๋ฅผ ๊ธฐ์ตํ๊ธฐ ์ด๋ ค์  
    โ ์ ๊ทผ ๊ถํ ๋ณ๋ก ์๋ก ๋ค๋ฅธ PW๋ฅผ ๋ถ์ฌ ํด์ผ ํจ
  - ์ค์ํ ํ์ผ์๋ ์ฌ์ฉํ๊ณ  ์์

  โก Access Matrix  
   : ๋ฒ์(domain)์ ๊ฐ์ฒด(object)์ฌ์ด์ ์ ๊ทผ ๊ถํ์ ๋ช์  
   โ domain: ์ฌ์ฉ์ / object: file ์ด๋ผ๊ณ  ์๊ฐํ๋ฉด ์ฌ์

  - Terminologies

    - Object : ์ ๊ทผ ๋์ (file, device ๋ฑ HW/SW objects)
    - Domain (protection domain)  
      โ ์ ๊ทผ ๊ถํ์ ์งํฉ, ๊ฐ์ ๊ถํ์ ๊ฐ์ง๋ ๊ทธ๋ฃน(์ฌ์ฉ์, ํ๋ก์ธ์ค)
    - Access right(์ ๊ทผ ๊ถํ)  
      โ \<object-name, right-set>

    <image src="https://www.researchgate.net/profile/Md-Kamrul-Hasan-4/publication/50346030/figure/tbl3/AS:667678335320072@1536198328582/Access-control-matrix.png" alt="access right" width="500px">

  - Implementation(๊ตฌํ ๋ฐฉ๋ฒ)

    - Global Table  
      : ์์คํ ์ ์ฒด file๋ค์ ๋ํ ๊ถํ์ Table๋ก ์ ์ง  
      โ table ํต์งธ๋ก ์ ์ฅํ๊ธฐ ๋๋ฌธ์ ๋น๊ณต๊ฐ๊น์ง ๊ฐ์ด ์ ์ฅํ๊ฒ ๋จ. ์ฆ size๊ฐ ์์ฒญ ์ปค์ง๐น๐น
    - Access list (๋น๊ณต๊ฐ ์ ์ฅx) - column ๋จ์ ์ ์ฅ  
      : Access matrix์ ์ด(column)์ list๋ก ํํ  
      โ ๊ฐ object์ ๋ํ ์ ๊ทผ ๊ถํ ๋์ด (ex. <D1, R1> <D2, R2>)  
      โ ๊ถํ์ด ์์ผ๋ฉด ์ ์ ์ด์ ๊ฐ ์์
      - Object ์์ฑ ์, ๊ฐ domain์ ๋ํ ๊ถํ ๋ถ์ฌ
      - Object ์ ๊ทผ ์ ๊ถํ์ ๊ฒ์ฌโจ
      - ์ค์  OS์์ ๋ง์ด ์ฌ์ฉ๋จ (UNIX ํฐ๋ฏธ๋์์ ls -l ํด๋ณด๋ฉด ์์ชฝ์์ ํ์ธ ๊ฐ๋ฅ)
      - ์์ฌ์ด์ ๐: ํ์ผ์ access ํ  ๋๋ง๋ค ์ฒดํฌํด์ผ ํ๋ overhead ๋ฐ์
    - Capability list (๋น๊ณต๊ฐ ์ ์ฅx) - row ๋จ์ ์ ์ฅ  
      : Access matrix์ ํ(row)์ list๋ก ์ ์ฅ  
      โ ๊ฐ domain์ ๋ํ ์ ๊ทผ ๊ถํ ๋์ด (ex. <F1, R1>, <F2, R2>) โ ์ ๋ถ์ฆ ๊ฐ์ ๋๋
      - Capability๋ฅผ ๊ฐ์ง์ด ๊ถํ์ ๊ฐ์ง์ ์๋ฏธ  
        โ ํ๋ก์ธ์ค๊ฐ ๊ถํ์ ์ ์, ์์คํ์ด ๊ฒ์ฆ ์น์ธ
      - ๐น๋จ์ : ์์คํ์ด capability list ์์ฒด๋ฅผ ๋ณดํธํด์ผ ํจ(kernel์์ ์ ์ฅ) โ overhead ๋ฐ์
    - Lock-key Mechanism  
      : Access list + Capability list ๊ฐ๋

      - Object๋ Lock์, Domain์ Key๋ฅผ ๊ฐ์ง
      - Domain ๋ด ํ๋ก์ธ์ค๊ฐ object์ ์ ๊ทผ ์, Domain์ key์ object์ lock ์ง์ด ๋ง์์ผ ํจ
      - ๐น์์คํ์ key list๋ฅผ ๊ด๋ฆฌํด์ผ ํจ(์ฌ์ ํ overhead ์กด์ฌ)

    - ๐ธ ๋น๊ต

      1. Global table : simple, but can be large
      2. Access list : Object ๋ณ ๊ถํ ๊ด๋ฆฌ ์ฉ์ด / ๋ชจ๋  ์ ๊ทผ ๋ง๋ค ๊ถํ ๊ฒ์ฌ ํ์(๋ง์ด ์ ๊ทผํ๋ฉด ๋๋ ค์ง)
      3. Capability list : List ๋ด object๋ค์ ๋ํ ์ ๊ทผ์ ์ ๋ฆฌ / ๐นObject ๋ณ ๊ถํ ๊ด๋ฆฌ(๊ถํ ์ทจ์ ๋ฑ)๊ฐ ์ด๋ ค์

    - ๐ธ ๊ฒฐ๋ก   
      : ๋ง์ OS๊ฐ Access list์ Capability list ๊ฐ๋์ ํจ๊ป ์ฌ์ฉ  
       โ Object์ ๋ํ ์ฒซ ์ ๊ทผ - access list ํ์ - ์ ๊ทผ ํ์ฉ ์ Capability ์์ฑ ํ ํด๋น ํ๋ก์ธ์ค์ ์ ๋ฌ(์ดํ ์ ๊ทผ ์์๋ ๊ถํ ๊ฒ์ฌ ๋ถํ์)- ๋ง์ง๋ง ์ ๊ทผ ํ Capability ์ญ์ 

### ๐Allocation Methods

> - Continuous allocation
> - Discontinuous allocation

1. Continuous Allocation  
   : ํ ํ์ผ์ ๋์คํฌ์ ์ฐ์๋ block์ ์ ์ฅ

- ๐์ฅ์ : ํจ์จ์ ์ธ file ์ ๊ทผ (์์ฐจ, ์ง์  ์ ๊ทผ)
- ๐น๋ฌธ์ ์ 
  - ์๋ก์ด file์ ์ํ ๊ณต๊ฐ ํ๋ณด๊ฐ ์ด๋ ค์
  - External fragmentation
  - File ๊ณต๊ฐ ํฌ๊ธฐ ๊ฒฐ์ ์ด ์ด๋ ค์  
    โ ํ์ผ์ด ์ปค์ ธ์ผ ํ๋ ๊ฒฝ์ฐ ๊ณ ๋ คํด์ผ ํจ

2. Discontinuous allocation

- 1. Linked Allocation

  - File์ด ์ ์ฅ๋ block๋ค์ linked list๋ก ์ฐ๊ฒฐ โ ๋น์ฐ์ ํ ๋น ๊ฐ๋ฅ
  - Directory๋ ๊ฐ file์ ๋ํ ์ฒซ ๋ฒ์งธ block์ ๋ํ ํฌ์ธํฐ๋ฅผ ๊ฐ์ง
  - Simple, No external fragmentation
  - ๐น๋จ์ 
    - ์ง์  ์ ๊ทผ์ ๋นํจ์จ์ 
    - ํฌ์ธํฐ(๋๋ ๋งํฌ) ์ ์ฅ์ ์ํ ๊ณต๊ฐ ํ์
    - ์ ๋ขฐ์ฑ ๋ฌธ์  โ ์ฌ์ฉ์๊ฐ ํฌ์ธํฐ๋ฅผ ์ค์๋ก ๊ฑด๋๋ฆฌ๋ ๋ฌธ์  ๋ฑ
  - ๋ง์ด ์ฐ์ โ **FAT**
    - File Allocation TAble (FAT) : ๊ฐ block์ ์์ ๋ถ๋ถ์ ๋ค์ ๋ธ๋ก์ ๋ฒํธ๋ฅผ ๊ธฐ๋กํ๋ ๋ฐฉ๋ฒ
    - MS-DOSm Windows ๋ฑ์ ์ฌ์ฉ ๋จ

- 2. Indexed Allocation (๋ชฉ์ฐจ๊ฐ ์๋ ๊ฒ!)
  - File์ด ์ ์ฅ๋ block์ ์ ๋ณด(pointer)๋ฅผ Index block์ ๋ชจ์ ๋ 
  - ์ง์  ์ ๊ทผ์ ํจ์จ์  (์์ฐจ ์ ๊ทผ์๋ ๋นํจ์จ์ )
  - file ๋น Index block์ ์ ์ง  
    โ Space overhead  
    โ Index block์ ํฌ๊ธฐ์ ๋ฐ๋ผ ํ์ผ์ ์ต๋ ํฌ๊ธฐ๊ฐ ์ ํ ๋จ
  - Unix ๋ฑ์ ์ฌ์ฉ ๋จ

### ๐Free Space Management(๋น ๊ณต๊ฐ ์ฐพ๊ธฐ!)

1. Bit Vector  
   : ์์คํ ๋ด ๋ชจ๋  block๋ค์ ๋ํ ์ฌ์ฉ ์ฌ๋ถ๋ฅผ 1 bit flag๋ก ํ์(๋นํธ๋งต)

   - Simple and efficient
   - Bit vector ์ ์ฒด๋ฅผ ๋ฉ๋ชจ๋ฆฌ์ ๋ณด๊ด ํด์ผ ํจ โ ๋ํ ์์คํ์ ๋ถ์ ํฉ(overhead)
     <image src="https://www.researchgate.net/profile/Zbigniew-Zielinski-2/publication/266615094/figure/fig3/AS:392083035705346@1470491288218/Bit-vector-transformation-to-a-set-of-arcs.png" width="500px" alt="bit vector">

2. Linked list  
   : ๋น block์ linked list๋ก ์ฐ๊ฒฐ โ ๊ณต๊ฐ, ์๊ฐ ๋ฉด์์ ๋ชจ๋ ๋นํจ์จ์ ๐น

3. Grouping  
   : n๊ฐ์ ๋น block์ ๊ทธ๋ฃน์ผ๋ก ๋ฌถ๊ณ , ๊ทธ๋ฃน๋จ์๋ก linked list๋ก ์ฐ๊ฒฐ

   - ์ฐ์๋ ๋น block์ ์ฝ๊ฒ ์ฐพ์ ์ ์์

4. Counting  
   : ์ฐ์๋ ๋น block๋ค ์ค ์ฒซ ๋ฒ์งธ block์ ์ฃผ์์ ์ฐ์๋ block์ ์๋ฅผ table๋ก ์ ์ง

- _Continuous allocation ์์คํ์ ์ ๋ฆฌํ ๊ธฐ๋ฒ_
