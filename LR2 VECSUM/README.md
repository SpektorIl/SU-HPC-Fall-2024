# Задание
### Сумма элементов вектора
**Задача:** реализовать алгоритм сложения элементов вектора  
**Язык:** C++ или Python  
**Входные данные:** Вектор размером 1 000...1 000 000 значений  
**Выходные данные:** сумма элементов вектора + время вычисления  
Реализация должна содержать 2 функции сложения элементов вектора: на CPU и на GPU с применением CUDA.

# Описание
Данная лабораторная работа была выполнена на языке Python в Jupyter Notebook.

**CPU:** функция `vecsum_cpu(vec)` принимает вектор (массив) vec и вычисляет его сумму, проходя по всем элементам с помощью цикла for. Результат возвращается как сумма всех элементов.

**GPU:** функция `gpu_sum_kernel` использует общий массив temp для хранения значений элементов вектора. Каждая нить (поток) загружает один элемент вектора в temp. Затем происходит редукция, где потоки попарно суммируют значения, пока не останется только одно значение. Наконец, результат суммируется атомарно, чтобы избежать конфликтов при записи. А функция `vecsum_gpu(vec)` создает массив для хранения результата и передает вектор и результат на GPU. Она определяет количество блоков и потоков, необходимых для выполнения CUDA-ядра, запускает его и возвращает результат обратно на CPU.

# Анализ результатов
Результаты выводятся в виде таблицы, где содержатся размеры векторов, время выполнения для CPU и GPU, а также коэффициент ускорения:
| Размер вектора | Время на CPU (с) | Время на GPU (с)  | Ускорение |
|----------------|------------------|-------------------|-----------|
| 1000           | 0.000000         | 0.533104          | 0.000000  |
| 5000           | 0.001001         | 0.000991          | 1.009865  |
| 10000          | 0.001505         | 0.001173          | 1.282724  |
| 50000          | 0.009485         | 0.001358          | 6.985426  |
| 100000         | 0.017475         | 0.000997          | 17.535167 |
| 500000         | 0.092032         | 0.000998          | 92.192739 |
| 1000000        | 0.276944         | 0.002244          | 123.428541|

Созданы графики, которые сравнивают время выполнения для CPU и GPU в зависимости от размера массива, а также график, показывающий ускорение вычислений на GPU по сравнению с CPU.  
![alt text](/assets/VECSUM-1.png)
![alt text](/assets/VECSUM-2.png)

Таким образом, код демонстрирует, как можно эффективно использовать GPU для ускорения операций суммирования по сравнению с традиционным подходом на CPU, и иллюстрирует разницу в производительности между двумя подходами.