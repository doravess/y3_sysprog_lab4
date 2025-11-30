# Лабораторна робота: Аналіз та вимір продуктивності
Лабораторна робота виконана на основі програми для Лабораторної роботи №4

---

## Компіляція
Створено дві версії програми: неоптимізована (-O0) та оптимізована (-O3).

### Нептимізована програма

gcc -g -O0 calculator_03 -o lab_program_unopt

### Оптимізована програма 

gcc -g -O3 -march=native calculator_03 -o lab_program_opt

---

# Аналіз неоптимізованої програми

### FlameGraph неоптимізованої програми 

<img width="724" height="355" alt="image" src="https://github.com/user-attachments/assets/40f7249c-eaa2-430f-b419-ad0d2ab083e0" />

---

## Збір статистики

### /usr/bin/time --verbose

<img width="895" height="441" alt="image" src="https://github.com/user-attachments/assets/edb16312-6f16-46fe-a857-9bee4f1a0a2d" />


### perf stat -d

<img width="911" height="470" alt="image" src="https://github.com/user-attachments/assets/5c08550c-82ec-42ad-8caf-5833471a5137" />


---

## Енерговитрати

### sudo perf stat -e power/energy-pkg/ ./lab_program_unopt

<img width="1257" height="163" alt="image" src="https://github.com/user-attachments/assets/b55fc29a-7068-481a-b00d-3cf1318ca743" />


---

# Аналіз оптимізованої програми

### FlameGraph оптимізованої програми 

<img width="726" height="448" alt="image" src="https://github.com/user-attachments/assets/ac855364-072e-4541-8d11-a5542d2b032d" />

---

## Збір статистики

<img width="916" height="439" alt="image" src="https://github.com/user-attachments/assets/4efc221d-ab78-4615-bbdf-395c835ec74d" />

<img width="906" height="470" alt="image" src="https://github.com/user-attachments/assets/93323322-78bb-4815-b147-79e09f4e88c9" />

---

## Енерговитрати

<img width="1234" height="157" alt="image" src="https://github.com/user-attachments/assets/2e354726-7eb4-4bd4-a3b0-0dede0493278" />

---

## Порівняльна таблиця неоптимізованої та оптимізованої програм

| Метрика                   | `calculator_O0` (-O0) | `calculator_O3` (-O3) | Зміна                      |
| :------------------------ | :-------------------- | :-------------------- | :------------------------- |
| **User time (`time`)**    | 0.22 с                | **0.17 с**            | **-22.7%**                 |
| **Cycles (`perf`)**       | ~1.015 млрд           | **~0.740 млрд**       | **-27.1%**                 |
| **Instructions (`perf`)** | ~2.683 млрд           | **~2.124 млрд**       | **-20.8%**                 |
| **IPC (`perf`)**          | 2.64                  | **2.87**              | **+8.7% (краще)**          |
| **L1-dcache-load-misses** | 0.03%                 | **0.04%**             | **+33% (трохи гірше)**     |
| **LLC-load-misses**       | 85.61%                | **86.29%**            | **+0.8% (майже без змін)** |

---

## Порівняльна таблиця енерговитрат

| Метрика                    | `calculator_O0` (-O0) | `calculator_O3` (-O3) | Зміна                                    |
| :------------------------- | :-------------------- | :-------------------- | :--------------------------------------- |
| **Час виконання**          | 0.23911 с             | **0.16079 с**         | **-32.8%**                               |
| **Енергія (pkg)**          | 4.82 Дж               | **3.35 Дж**           | **-30.5%**                               |
| **Енергія (cores)**        | 4.29 Дж               | **3.29 Дж**           | **-23.3%**                               |
| **Середня потужність CPU** | 17.1 Вт               | **20.8 Вт**           | **+21.6% (вище через швидше виконання)** |







