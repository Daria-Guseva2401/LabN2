## Отчет по лабораторной работе № 2

#### № группы: `ПМ-2101`

#### Выполнилa: `Гусева Дарья Борисовна`

#### Вариант: `9`

### Cодержание:

- [Постановка задачи](#1-постановка-задачи)
- [Входные и выходные данные](#2-входные-и-выходные-данные)
- [Алгоритм](#3-алгоритм)
- [Программа](#4-программа)
- [Анализ правильности решения](#5-анализ-правильности-решения)

### 1. Постановка задачи

> Напишите программу на Java, которая выполняет следующие действия с одномерным массивом строк:
>1. Считывает с консоли число N, затем N строк и заполняет массив размером N.
>2. Упорядочивает строки по количеству слов в них. Если количество слов одинаковое, сортирует в порядке возрастания
>   числа гласных букв. Если и это одинаково, сортирует строки по длине.
>3. Находит и выводит самую часто встречающуюся букву во всех
>   строках (без учёта регистра). Если таких букв несколько, выводит все.
>4. Соединяет все строки в одну, разделяя их запятыми, если строка не заканчивается знаком препинания.
>   Затем подсчитывает количество слов в полученной строке и выводит результат   


Данную задачу можно разделить на 4 подзадачи: для каждого пункта

- Для 1 подзадачи нужно создать массив из строк и заполнить его с консоли
- Для 2 подзадачи нужно отсортировать строки исходя из количества слов в них, либо по числу гласных, либо по их длине
- Для 3 подзадачи нужно посмотреть сколько раз каждая из букв встречается в строках и вывести их
- Для 4 подзадачи нужно соеденить строки в одну и поставить между ними запятые если они
  не оканчиваются на знаки препинания и подсчитать количество слов в этой строке

### 2. Входные и выходные данные

#### Данные на вход

На вход программа должна получать одно число, являющееся количеством строк, то есть оно должно быть натуральным(int).
затем программа получает некоторе количество строк(тип String).

#### Данные на выход

Программа должна выводить эти же строки в отсортированном порядке(тип String), так же она должна вывести самую часто встречающуюся
букву которая будет храниться в типе char. Финальная строка и количество слов в ней будут так же храниться в типе String и int соответственно

### 3. Алгоритм

#### Алгоритм выполнения программы:

1. **Ввод данных:**  
   Программа считывает натуральное число N а затем заполняет массив a размером N+1 строками 

2. **Первый пункт:**  
   Программа с помощью цикла for проходиться по всем строкам массива и сохраняет в переменные x и y текущую строку и идущую за ней чтобы стравнить их между собой.
   сначала мы разделяем строки x и y по пробелам и считаем длинну полученного массива из слов чтобы узнать их количество. если количество слов в текущей строке больше
   чем в следующей после нее то мы меняем их местами. если же количество слов одинакого, то мы сравниваем количество гласных. для этого мы создаем отдельный массив
   'g' который хранит все номера гласных из Unicode а затем сравниваем каждый символ строки с этим массивом, фиксируя это число в переменные k1 и k2. если же и число гласных одинаково, то мы просто сравниваем длину двух строчек и таким образом с помощью метода пузырька сортируем массив.

4. **Второй пункт:**
    для определения самой часто встречающейся буквы мы создаем строку s состоящую из алфавита а затем создаем массив символов l который заполяем символами из строки s. так 
    же мы создаем массив с в котором будем хранить информацию о том сколько какая буква раз встречается и заполняем его нулями. далее мы с помощью цикла for делаем все 
    строки с нижним регистром(т.к. в задании указано не учитывать регистр) а затем так же как и с гласными сравниваем каждый символ в строке с элементами массива l, и при 
    обнаружении совпадения прибавляем к соответствующему элементу массива с еденицу(номер буквы в массиве l совпадает с номером его количества в массиве с).
   затем мы ищем максимальное число в массиве с чтобы узнать какое максимальное число повторений у букв. после этого мы сравниваем это число со всеми числами в массиве с
   и при обнаружении совпадений выводим элемент из массива l с таким же порядковым номером.
2. **Третий пункт:**  
   чтобы объеденить все строки мы создаем пустую строку o(куда в последующем будем добавлять остальные строки) и с помощью цикла for проходимся по всем строкам и проверяем 
   их: вводим переменную u типа String в которой храним текущую строку, а затем вводим переменную h типа int в которой храним длинну нашей строки минус 1(это будет индекс 
   последнего элемента). далее мы проверяем является ли последний символ знаком препинания, если нет и при этом это не последняя строка, то мы прибавляем эту строку к строке
   o и после нее ещё добавдяем запятую, если же эти условия не соблюдаются то мы просто добавляем строку и идем дальше. после объединения всех строк в одну мы создаем 
   переменную n и даем ей значение длины массива строки o разделенной по пробелам, так мы и узнаем число слов.
   
6. **Вывод результата:**  
   На экран выводится сначала отсортированные строки, затем самые часто встречающиеся буквы, затем одна объединённая строка и количество слов в ней.

### 4. Программа

```java
import java.io.PrintStream;
import java.util.Scanner;
public class Main {
    public static Scanner in = new Scanner(System.in);
    public static PrintStream out = System.out;
    public static void main(String[] args) {
        int N = in.nextInt(); //пользователь вводит количество строк
        String []a = new String[N+1]; //создаем массив строк 
        for(int i = 0; i<N+1; i++) {
            a[i] = in.nextLine();     //пользователь вводит строки
        }
        int []g = new int[13];  //создаем массив для хранения всех гласных букв
        g[0] = 65; g[1] = 69; g[2]=73; g[3]=79; g[4]=85; g[5]=89; g[6]=97; g[8]=101; g[9]=105; g[10]=111; g[11]=117; g[12]=121; //заполняем его номерами гласных букв в кодировке Unicode
        String s = "abcdefghijklmnopqrstuvwxyz"; //создаем строчку состоящую из алфавита 
        char []l = new char[s.length()]; //создаем массив в котором будет храниться алфавит
        for(int i = 0; i<s.length();i++){
            l[i] = s.charAt(i); //посимвольно заполняем массив строчкой s 
        }
        int []c = new int[s.length()]; //создаем массив в котором будет храниться встречаемость каждой буквы во всех строчках
        for(int i = 0; i<s.length(); i++){
            c[i] = 0;  //для старта заполним его нулями
        }
        String o = " "; //создаем строчку в которой будем объединять все остальные для последнего пункта
        for(int i = 0; i < N; i++){
            String x = a[i]; //создаем переменную для операции с строкой
            String y = a[i+1]; //создаем вторую переменную для второй строки чтобы сравнить их
            if(((x.split(" ")).length)>((y.split(" ")).length)){ //разделяем строчки по пробелам и смотрим их длину, 
                String q = a[i];  //считая так количество слов и если у первой строки слов больше чем во второй 
                a[i] = a[i+1]; //то меняем их местами, то есть сортируем их методом пузырька
                a[i+1] = q;
            }
            if(((x.split(" ")).length)==((y.split(" ")).length)) { //если количество слов одинаково, переходим к 
                int k1 = 0; //следующему критерию сравнения
                int k2 = 0; //создаем переменные для хранения количества гласных
                for(int j = 0; j < a[i].length(); j++){
                    for(int r = 0; r < 13; r++){
                    if(a[i].charAt(j)==g[r]){ //далее сравниваем каждый символ строки с элементами массива с гласными
                    k1+=1;}  //и при совпадении увеличиваем счетчик
                    }
                }
                for(int j = 0; j < a[i+1].length(); j++){
                    for(int r = 0; r < 13; r++){
                        if(a[i+1].charAt(j)==g[r]){ //то же самое проделываем для второй строки 
                            k1+=1;}
                    }
                }
                if(k1>k2){ //сравниваем количество гласных и так же сортируем при необходимости
                    String q = a[i];
                    a[i] = a[i+1];
                    a[i+1] = q;
                }
                if(k1==k2) { //если и количество гласных равно то сравниваем их по длине
                    if(a[i].length()>a[i+1].length()) {
                        String q = a[i];
                        a[i] = a[i+1];
                        a[i+1] = q;
                    }
                }
            }

        }
        for(int i = 0; i<N+1; i++){
            out.println(a[i]);  //выводим отсортированные строки
        }
        for(int i = 0; i<N+1; i++) {
            a[i] = a[i].toLowerCase();  //понижаем регистр всех символов для удобства
            for (int j = 0; j < a[i].length(); j++) {
                for (int r = 0; r < s.length(); r++) {
                    if (a[i].charAt(j) == l[r]) {  //сравниваем каждый символ всех строк с массивом с алфавитом
                        c[r] += 1; //при обнаружении совпадений добавляем в массив с счетчиком букв еденицу к соответствующему букве индексу 
                    }
                }
            }
        }
        int z = c[0];
        for(int i = 0; i<s.length(); i++){
            if(c[i]>z) {
                z = c[i];   //ищем максимальный элемент в счетчике встречаемости букв
            }
        }
        out.println("самые частые буквы:");
        for(int i = 0; i<s.length(); i++){
            if(z==c[i]){
                out.print(l[i]+" "); //выводим все буквы с таким показателем счетчика 
            }
        }
        out.println(" ");
        for(int i = 0; i<N+1; i++){
            String u = a[i];  //вводим отдельную переменную для хранения строки
            int h = u.length() - 1;  //вводим переменную для хранения длины строки - 1, это будет индекс последнего 
                if(((a[i].charAt(h)!=33)||(a[i].charAt(h)!=44)||(a[i].charAt(h)!=46)||(a[i].charAt(h)!=58)||(a[i].charAt(h)!=59)||(a[i].charAt(h)!=63))&&(i!=N)){  //проверяем условие чтобы последний символ строки не был знаком препинания и при этом не был последний
                    o += a[i]; //добавляем строку к одной чтобы объеденить их 
                    o += ",";  //добавляем запятую для соединения строк
            }
                else {
                    o += a[i];  //если строка и так заканчивается на знак препинания то мы просто добавляем строку
                }
            int n = (o.split(" ")).length;  //считаем количество слов в строке 
                out.print(o+" "+n);  //выводим цельную строку и количество слов в ней 

        }


    }}
```

### 5. Анализ правильности решения

Программа работает корректно на всем множестве решений с учетом ограничений.

1. Тест на сортировку по количеству слов и определение букв:

    - **Input**:
        ```
        2
        dergth ewret
        wdfedrg
        ```

    - **Output**:
        ```
        wdfedrg
        dergth ewret
        самые частые буквы:
        e
        wdfedrg, dergth ewret 3
        ```

2. Тест на сортировку по гласным и нескольким самым частым буквам:

    - **Input**:
        ```
        3
        aaaaa sdfggh
        dfgh fgh
        g
        ```

    - **Output**:
        ```
        g
        dfgh fgh
        aaaaa sdfggh
        самые частые буквы:
        a g
        g, dfgh fgh, aaaaa sdfggh 5
        ```

3. Тест на сортировку по длине и знаки препинания:

    - **Input**:
        ```
        2
        aaaagggg
        aaaa;
        ```

    - **Output**:
        ```
        aaaa;
        aaaagggg
        самые частые буквы:
        a
        aaaa; aaaagggg 2
        ```
