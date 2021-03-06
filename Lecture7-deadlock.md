## Lecture 7. Deadlock Resolution

### κ΅μ°©μν

---

### πDeadlockμ κ°λ

- Blocked/Asleep state  
  β νλ‘μΈμ€κ° 'νΉμ  μ΄λ²€νΈ' νΉμ 'νμν μμ'μ κΈ°λ€λ¦¬λ μν
- Deadlock state  
  β νλ‘μΈμ€κ° **λ°μ κ°λ₯μ±μ΄ μλ μ΄λ²€νΈ**λ₯Ό κΈ°λ€λ¦¬λ κ²½μ°(νλ‘μΈμ€κ° deadlock μν)  
  β μμ€ν λ΄μ deadlockμ λΉ μ§ νλ‘μΈμ€κ° μλ κ²½μ°(μμ€νμ΄ deadlock μν)
- starvationκ³Ό μ μ¬  
  β starvationμ cpuλ₯Ό κΈ°λ€λ¦¬κ³  ready stateμ μμΌλ©°, λ°μ κ°λ₯μ±μ΄ μλ κ²μ μλλΌλ μ μμ μ°¨μ΄κ° μλ€.

### πμμμ λΆλ₯

- μΌλ°μ  λΆλ₯ : Hardware resources vs Software resources
- λ€λ₯Έ λΆλ₯λ²
  - μ μ  κ°λ₯ μ¬λΆμ λ°λ₯Έ λΆλ₯
  - ν λΉ λ¨μμ λ°λ₯Έ λΆλ₯
  - λμ μ¬μ© κ°λ₯ μ¬λΆμ λ°λ₯Έ λΆλ₯
  - μ¬μ¬μ© κ°λ₯ μ¬λΆμ λ°λ₯Έ λΆλ₯

1. **μ μ  κ°λ₯ μ¬λΆ**μ λ°λ₯Έ λΆλ₯

   - preemptible resources  
     β μ μ  λΉν ν, λμμλ λ¬Έμ κ° λ°μνμ§ μλ μμ  
     β Processor, memory λ±
   - Non-preemptible resources  
     β μ μ  λΉνλ©΄, μ΄ν μ§νμ λ¬Έμ κ° λ°μνλ μμ - Rollback, restart λ± νΉλ³ν λμμ΄ νμ  
     β E.g., disk drive λ±

2. **ν λΉ λ¨μ**μ λ°λ₯Έ λΆλ₯

   - Total allocation resources  
     β μμ μ μ²΄λ₯Ό νλ‘μΈμ€μκ² ν λΉ  
     β E.g., Processor, disk drive λ±
   - Partitioned allocation resources  
     β νλμ μμμ μ¬λ¬ μ‘°κ°μΌλ‘ λλμ΄ μ¬λ¬ νλ‘μΈμ€λ€μκ² ν λΉ  
     β E.g., Memory λ±

3. **λμ μ¬μ©κ°λ₯ μ¬λΆ**μ λ°λ₯Έ λΆλ₯

   - Exclusive allocation resources  
     β ν μκ°μ ν νλ‘μΈμ€λ§ μ¬μ© κ°λ₯  
     β E.g., Processor, memory, disk drive λ±  
     β λ©λͺ¨λ¦¬μ κ²½μ° μ¬λ¬ μ‘°κ°μΌλ‘ ν λΉνμ§λ§ ν΄λΉ μ‘°κ° νλνλλ ν μκ°μ ν νλ‘μΈμ€λ§ μ¬μ© κ°λ₯νλ€.
   - Shared allocation resource  
     β μ¬λ¬ νλ‘μΈμ€κ° λμμ μ¬μ© κ°λ₯ν μμ  
     β E.g., Program(sw), shared data λ±

4. **μ¬μ¬μ© κ°λ₯ μ¬λΆ**μ λ°λ₯Έ λΆλ₯
   - SR (Serially-reusable Resources)  
     β μμ€ν λ΄μ ν­μ μ‘΄μ¬νλ μμ  
     β μ¬μ©μ΄ λλλ©΄, λ€λ₯Έ νλ‘μΈμ€κ° μ¬μ© κ°λ₯  
     β E.g., Processor, memory, disk drive, program λ±
   - CR (Consumable Resources)  
     β ν νλ‘μΈμ€κ° μ¬μ©ν νμ μ¬λΌμ§λ μμ  
     β E.g., signal, message λ±

### πDeadlockκ³Ό μμμ μ’λ₯

- Deadlockμ λ°μμν¬ μ μλ μμμ ννβ¨
  - Non-preemptible resources
  - Exclusive allocation resources
  - Serially reusable resources  
    β» ν λΉ λ¨μλ μν₯μ λ―ΈμΉμ§ μμ!
- CRμ λμμΌλ‘ νλ Deadlock modelκΉμ§ μκ°νλ©΄ λλ¬΄ λ³΅μ‘! => λΉΌκ³  μκ°

### πDeadlock Model (ννλ²)

1. **Graph Model**

   - Nodeμ Edgeλ‘ κ΅¬μ±
     - Node : νλ‘μΈμ€ λΈλ(P1, P2) μμ λΈλ(R1, R2)
     - Edge  
       β Rj => Pi : μμ Rjμ΄ νλ‘μΈμ€ Piμ ν λΉ λ¨  
       β Pi => Rj : νλ‘μΈμ€ Piκ° μμ Rjμ μμ²­(λκΈ° μ€)
   - cycleμ΄ λ§λ€μ΄μ§λ©΄ deadlock

2. **State Transition Model**

### πDeadlock λ°μ νμ μ‘°κ±΄β¨

(μμμ νΉμ±)

- Exclusive use of resources
- Non-preemptible resources

(νλ‘μΈμ€μ νΉμ±)

- Hold and wait (Partial allocation)
- Circular wait

Deadlock ν΄κ²°λ°©λ² ?  
=> **Deadlock νμ μ‘°κ±΄ μ€ νλλ₯Ό ν΄κ²°νλ©΄ λ¨**

### πDeadlock ν΄κ²° λ°©λ²

- Deadlock _prevention_ methods
  β κ΅μ°©μν _μλ°©_
- Deadlock _avoidance_ method  
  β κ΅μ°©μν _ννΌ_
- Deadlock _detection_ and deadlock _recovery_ methods  
  β κ΅μ°©μν _νμ§ λ° λ³΅κ΅¬_

### πDeadlock prevention

- Deadlockμ΄ μ λ λ°μνμ§ μλλ‘ νλ κ²
- μμ μΈκΈν **deadlock λ°μ νμ μ‘°κ±΄ μ€ νλλ₯Ό μ κ±°**
- μ¬κ°ν μμ λ­λΉ λ°μ  
  β Low device utilization  
  β Reduced system throughput
- λΉνμ€μ β¨

1. λͺ¨λ  μμμ κ³΅μ  νμ©  
   β Exclusive use of resources μ‘°κ±΄ μ κ±°  
   β νμ€μ μΌλ‘ λΆκ°λ₯

2. λͺ¨λ  μμμ λν΄ μ μ  νμ©  
   β Non-preemptible resources μ‘°κ±΄ μ κ±°  
   β νμ€μ μΌλ‘ λΆκ°λ₯  
   β μ μ¬ν λ°©λ² : νλ‘μΈμ€κ° ν λΉ λ°μ μ μλ μμμ μμ²­ν κ²½μ°, κΈ°μ‘΄μ κ°μ§κ³  μλ μμμ λͺ¨λ λ°λ©νκ³  μμ μ·¨μ(μ΄ν μ²μ(or check point)λΆν° λ€μ μμ)  
   β μ¬κ°ν μμ λ­λΉ λ°μ => λΉνμ€μ 

3. νμ μμ νλ²μ λͺ¨λ ν λΉ (Total allocation)  
   β Hold and wait μ‘°κ±΄ μ κ±°  
   β μμ λ­λΉ λ°μ => νμνμ§ μμ μκ°μλ κ°κ³  μμ  
   β λ¬΄ν λκΈ° νμ λ°μ κ°λ₯

4. Circular wait μ‘°κ±΄ μ κ±°  
   β Totally allocationμ μΌλ°ν ν λ°©λ²  
   β μμλ€μκ² μμλ₯Ό λΆμ¬  
   β νλ‘μΈμ€λ μμμ μ¦κ° λ°©ν₯μΌλ‘λ§ μμ μμ²­ κ°λ₯β¨  
   β μμ λ­λΉ λ°μ

### πDeadlock avoidance

β μμ€νμ μνλ₯Ό κ³μ κ°μ  
 β μμ€νμ΄ **deadlock μνκ° λ  κ°λ₯μ±**μ΄ μλ μμ ν λΉ μμ²­ λ³΄λ₯  
 β μμ€νμ ν­μ **safe state**λ‘ μ μ§

- Safe state  
  β **λͺ¨λ  νλ‘μΈμ€κ° μ μμ  μ’λ£ κ°λ₯ν μν**  
  β Safe sequenceκ° μ‘΄μ¬ => Deadlockμνκ° λμ§ μμ μ μμμ μ‘΄μ¬
- Unsafe state  
  β Deadlock μνκ° λ  **κ°λ₯μ±**μ΄ μμ  
  β λ°λμ λ°μνλ€λ μλ―Έλ μλ!!

- π©βπκ°μ  (Not practicalν¨)  
  β νλ‘μΈμ€μ μκ° κ³ μ   
  β μμμ μ’λ₯μ μκ° κ³ μ λ¨  
  β νλ‘μΈμ€κ° μκ΅¬νλ μμ λ° μ΅λ μλμ μκ³  μμ  
  β νλ‘μΈμ€λ μμμ μ¬μ© ν λ°λμ λ°λ© (\_λΉμ°ν μ΄μΌκΈ°)

- λ°©λ²

  1. Dijkstra's algorithm - banker's algorithm

     - Deadlock avoidanceλ₯Ό μν κ°λ¨ν μ΄λ‘ μ  κΈ°λ²
     - κ°μ  : ν μ’λ₯(resource type)μ μμμ΄ μ¬λ¬ κ°(unit)
     - μμ€νμ ν­μ safe stateλ‘ μ μ§  
       => μμ μμ²­μ΄ λ€μ΄μμ λ λΉλ €μ€¬λ€κ³  κ°μ νκ³  safe stateκ° μλμ§ νμΈ

  2. Habermann's algorithm
     - Dijkstra's algorithmμ νμ₯
     - μ¬λ¬ μ’λ₯μ μμ κ³ λ €β¨
     - μμ€νμ ν­μ safe stateλ‘ μ μ§  
       <img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2016/01/safety.png" alt="deadlock avoidance" width="500px">

- πDeadlock Avoidance μ λ¦¬
  - Deadlockμ λ§μ μ μμ
  - High overhead : ν­μ μμ€νμ κ°μνκ³  μμ΄μΌ ν¨
  - Low resource utilization : safe state μ μ§λ₯Ό μν΄ μ¬μ© λμ§ μλ μμμ΄ μ‘΄μ¬
  - Not practical : νλ‘μΈμ€ μ, μμ μκ° κ³ μ . νμν μ΅λ μμ μλ₯Ό μκ³ μμ

### πDeadlock detection

- Deadlock λ°©μ§λ₯Ό μν μ¬μ  μμμ νμ§ μμ(Deadlock λ°μ κ°λ₯)
- μ£ΌκΈ°μ μΌλ‘ deadlock λ°μ νμΈ
  - μμ€νμ΄ deadlock μνμΈκ°?
  - μ΄λ€ νλ‘μΈμ€κ° deadlock μνμΈκ°?
- Resource Allocation Graph (RAG) μ¬μ©  
  <img src="https://courses.cs.washington.edu/courses/cse451/98au/Lectures/9-deadlock/img005.JPG" width="500px" alt="RAG">
  - Graph reduction (DeadlockμΈμ§ νμΈνλ λ²)  
    : μ£Όμ΄μ§ RAGμμ edgeλ₯Ό νλμ© μ§μκ°λ λ°©λ²
    - Completly reduced : λͺ¨λ  edge μ κ±°λ¨. Deadlockμ λΉ μ§ νλ‘μΈμ€ μμ.
    - Irreducible : μ§μΈ μ μλ edgeκ° μ‘΄μ¬. νλ μ΄μμ νλ‘μΈμ€κ° deadlock μν.
    - νΉμ§  
      β High overhead : κ²μ¬ μ£ΌκΈ°μ μν₯ λ°μ / Nodeμ μκ° λ§μ κ²½μ°

### πDeadlock Avoidance vs Detection

- Deadlock avoidance

  - μ΅μμ κ²½μ°λ₯Ό μκ° - μμΌλ‘ μΌμ΄λ  μΌμ κ³ λ €
  - Deadlockμ΄ λ°μνμ§ μμ

- Deadlock detection
  - μ΅μ μ κ²½μ°λ₯Ό μκ° - νμ¬ μνλ§ κ³ λ €
  - Deadlock λ°μ μ Recovery κ³Όμ μ΄ νμ

### πDeadlock Recovery

- λ κ°μ§ λ°©λ²

  - Process termination

    - Deadlock μνμΈ νλ‘μΈμ€ μ€ **μΌλΆ** μ’λ£
    - Termination cost model : μ’λ£ μν¬ deadlock μνμ νλ‘μΈμ€ μ ν  
      β Termination cost

      - μ°μ μμ / The priority
      - μ’λ₯ / Process type
      - μ΄ μν μκ° / Accumulated execution time of the process
      - λ¨μ μν μκ° / Remaining time of the process
      - μ’λ£ λΉμ© / Accounting cost
      - Etc.

    - Lowest-termination cost process first  
      β simple  
      β Low overhead  
      β λΆνμν νλ‘μΈμ€λ€μ΄ μ’λ£ λ  κ°λ₯μ±μ΄ λμ

    - Minimum cost recovery  
      β μ΅μ λΉμ©μΌλ‘ deadlock μνλ₯Ό ν΄μ ν  μ μλ process μ ν  
      β λͺ¨λ  κ²½μ°μ μλ₯Ό κ³ λ €ν΄μΌ νλ―λ‘ complex, high overhead  
      β O(2^k)

  - Resource preemption

    - Deadlock μν ν΄κ²°μ μν΄ μ μ ν  μμ μ ν
    - ν΄λΉ μμμ κ°μ§κ³  μλ νλ‘μΈμ€λ₯Ό μ’λ£ μν΄  
      β Deadlock μνκ° μλ νλ‘μΈμ€κ° μ’λ£ λ  μλ μμπ±π±  
      β ν΄λΉ νλ‘μΈμ€λ μ΄ν μ¬μμ λ¨
    - μ μ ν  μμ μ ν  
      β Preemtion cost modelμ΄ νμ  
      β Minimum cost recovery method μ¬μ©  
      β O(r)

  - Checkpoint-restart method
    - νλ‘μΈμ€μ μν μ€ **νΉμ  μ§μ (checkpoint)λ§λ€ contextλ₯Ό μ μ₯**
    - Rollbackμ μν΄ μ¬μ© : κ°μ  μ’λ£ ν κ°μ₯ μ΅κ·Όμ checkpointμμ μ¬μμ
