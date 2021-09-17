

1.Что такое лямбда-выражение?  
**Ответ.** В функциональном языке lambda-выражения – это функции; но в Java, lambda-выражения – представляются объектами, и должны быть связаны с конкретным объектным типом, который называется функциональный интерфейс.
Лямбда-выражения, по сути, это анонимный класс или метод.  
**Источник.**https://javarush.ru/groups/posts/845-lambda-vihrazhenija-na-primerakh
https://habr.com/ru/post/512730/


2.Из каких элементов состоит объявление лямбда-выражения?  
**Ответ.** Lambda-выражения в Java обычно имеют следующий синтаксис (аргументы) -> (тело). Например:
(int a, int b) -> {  return a + b; }  
**Источник.** https://javarush.ru/groups/posts/845-lambda-vihrazhenija-na-primerakh


3.При объявлении лямбда-выражения какие структуры можно опустить?  
**Ответ.** Lambda-выражения – это анонимные функции (может и не 100% верное определение для Java, но зато привносит некоторую ясность). Проще говоря, это метод без объявления, т.е. без модификаторов доступа, возвращающие значение и имя.  
**Источник.** https://javarush.ru/groups/posts/845-lambda-vihrazhenija-na-primerakh

4.Что такое поток и конвейер в контексте лямбда-выражения?  
**Ответ.**Поток - это последовательность элементов.Конвейер - это последовательность потоковых операций.
 **Источник.**https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#approach9

5.Какие компоненты содержит конвейер?  
**Ответ.** Конвейер содержит следующие компоненты:

   - Источник: это может быть коллекция, массив, функция генератора или канал ввода-вывода. В этом примере источником является список коллекции.

   - Ноль или более промежуточных операций. Промежуточная операция, такая как фильтр, создает новый поток.

   - Поток - это последовательность элементов. В отличие от коллекции, это не структура данных, в которой хранятся элементы. Вместо этого поток передает значения из источника по конвейеру. В этом примере создается поток из списка коллекций путем вызова метода stream.

   - Операция фильтра возвращает новый поток, содержащий элементы, соответствующие его предикату (параметру этой операции). В этом примере предикатом является лямбда-выражение e -> e.getGender () == Person.Sex.MALE. Он возвращает логическое значение true, если поле пола объекта e имеет значение Person.Sex.MALE. Следовательно, операция фильтрации в этом примере возвращает поток, который содержит всех мужчин-членов в списке сбора.

   - Терминальная операция. Терминальная операция, такая как forEach, дает результат, не являющийся потоком, например примитивное значение (например, двойное значение), коллекцию или, в случае forEach, вообще никакого значения. В этом примере параметром операции forEach является лямбда-выражение e -> System.out.println (e.getName ()), которое вызывает метод getName для объекта e. (Среда выполнения и компилятор Java делают вывод, что тип объекта e - Person.)  
   **Источник.** https://docs.oracle.com/javase/tutorial/collections/streams/index.html 


6.Что такое агрегатные операции? Приведите примеры агрегатных операций.  
**Ответ.**
```java
roster
    .stream()
    .filter(
        p -> p.getGender() == Person.Sex.MALE
            && p.getAge() >= 18
            && p.getAge() <= 25)
    .map(p -> p.getEmailAddress())
    .forEach(email -> System.out.println(email));
```
Операции filter, map и forEach являются агрегатными операциями.(Потоковые операции) Агрегированные операции обрабатывают элементы из потока, а не напрямую из коллекции.   
**Источник.**https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#approach9
    

7.Какие различия между агрегатными операциями и итераторами?  
**Ответ.**Агрегатные операции, такие как forEach, похожи на итераторы. Однако у них есть несколько принципиальных отличий:

   - Они используют внутреннюю итерацию: агрегатные операции не содержат такого метода, как next, для указания им обработать следующий элемент коллекции. При внутреннем делегировании ваше приложение определяет, какую коллекцию оно выполняет, но JDK определяет, как выполнять итерацию коллекции. При внешней итерации ваше приложение определяет как итерацию коллекции, так и способ ее выполнения. Однако внешняя итерация может выполнять итерацию только по элементам коллекции последовательно. Внутренняя итерация не имеет этого ограничения. Он может более легко использовать преимущества параллельных вычислений, которые включают разделение проблемы на подзадачи, одновременное решение этих проблем, а затем объединение результатов решений подзадач. См. Раздел Параллелизм для получения дополнительной информации.

   - Они обрабатывают элементы из потока: агрегированные операции обрабатывают элементы из потока, а не напрямую из коллекции. Следовательно, их еще называют потоковыми операциями.

   - Они поддерживают поведение как параметры: вы можете указать лямбда-выражения как параметры для большинства агрегированных операций. Это позволяет вам настроить поведение конкретной агрегированной операции.   
   **Источник.** https://docs.oracle.com/javase/tutorial/collections/streams/index.html#differences


8.Какие имеются ограничения на локальные переменные, которые используются в лямбда-выражениях?  
**Ответ.** Лямбда-выражение может использовать переменные, которые объявлены во вне в более общей области видимости - на уровне класса или метода, в котором лямбда-выражение определено. Переменные  объявлены на уровне класса, и в лямбда-выражении мы их можем получить и даже изменить. Локальные переменные уровня метода мы также можем использовать в лямбдах, но изменять их значение нельзя.Более того, мы не сможем изменить значение переменной, которая используется в лямбда-выражении, вне этого выражения. То есть даже если такая переменная не объявлена как константа, по сути она является константой.  
**Источник.** https://metanit.com/java/tutorial/9.1.php


9.Что такое целевой тип лямбда-выражения и как компилятор определяет целевой тип?  
**Ответ.**Функциональный интерфейс определяет целевой тип лямбда-выражения. Вот ключевой момент: лямбда-выражение можно использовать только в контексте, в котором указан его целевой тип.
Можно сказать, что результат, который намеревается достичь лямбда-выражение, - это реализация какого-то функционального интерфейса. Следовательно, этот функциональный интерфейс может рассматриваться как цель этого лямбда-выражения, а тип функционального интерфейса - это целевой тип.  
**Источник.** https://overcoder.net/q/1183915/%D1%87%D1%82%D0%BE-%D0%BF%D0%BE%D0%B4%D1%80%D0%B0%D0%B7%D1%83%D0%BC%D0%B5%D0%B2%D0%B0%D0%B5%D1%82%D1%81%D1%8F-%D0%BF%D0%BE%D0%B4-%D1%86%D0%B5%D0%BB%D0%B5%D0%B2%D1%8B%D0%BC-%D1%82%D0%B8%D0%BF%D0%BE%D0%BC-%D0%BB%D1%8F%D0%BC%D0%B1%D0%B4%D0%B0-%D0%B8-%D0%BA%D0%BE%D0%BD%D1%82%D0%B5%D0%BA%D1%81%D1%82%D0%BE%D0%BC-%D1%86%D0%B5%D0%BB%D0%B5%D0%B2%D0%BE%D0%B3%D0%BE-%D1%82%D0%B8%D0%BF%D0%B0-%D0%B2-java


10.В каких ситуациях может использоваться лямбда-выражение?  
**Ответ.** Лямбда-выражения могут использоваться только в том случае, если вам нужно переопределить не более одного метода.   
**Источник.**https://habr.com/ru/post/419395/


11.Могут ли лямбда-выражения ссылаться на другие существующие методы? Если да - приведите пример.  
**Ответ.** Да, могут.
```java
Person[] rosterAsArray = roster.toArray(new Person[roster.size()]);

class PersonAgeComparator implements Comparator<Person> {
    public int compare(Person a, Person b) {
        return a.getBirthday().compareTo(b.getBirthday());
    }
}
        
Arrays.sort(rosterAsArray, new PersonAgeComparator());


Arrays.sort(rosterAsArray,
    (a, b) -> Person.compareByAge(a, b)
);



Arrays.sort(rosterAsArray, Person::compareByAge);
```
Ссылка на метод Person :: compareByAge семантически совпадает с лямбда-выражением (a, b) -> Person.compareByAge (a, b). Каждый из них имеет следующие характеристики:

   - Его формальный список параметров копируется из Comparator <Person> .compare, то есть (Person, Person).
   - Его тело вызывает метод Person.compareByAge.   
**Источник.** https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html   


12.Укажите виды ссылок на методы в контексте лямбда-выражений и приведите соответствующие пример.  
**Ответ.** 
```java
- Ссылка на статический метод \ContainingClass::staticMethodName\   Person::compareByAge
                                                                    MethodReferencesExamples::appendStrings
- Ссылка на метод экземпляра конкретного объекта  \containingObject::instanceMethodName \   myComparisonProvider::compareByName
                                                                                            myApp::appendStrings2
- Ссылка на метод экземпляра произвольного объекта определенного типа \ ContainingType::methodName\  String::compareToIgnoreCase
                                                                                                      String::concat
- Ссылка на конструктор  \ 	ClassName::new\ HashSet::new 
```  
**Источник.**https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html                                                                                                                                                                                                  	                                                                    


13.Что такое операции сокращения в контексте лямбда-выражений?  
**Ответ.**JDK содержит множество терминальных операций (таких как среднее, сумма, минимальное, максимальное и количество), которые возвращают одно значение путем объединения содержимого потока. Эти операции называются операциями редукции. JDK также содержит операции сокращения, которые возвращают коллекцию вместо одного значения. Многие операции сокращения выполняют конкретную задачу, такую как поиск среднего значения или группирование элементов по категориям.   
**Источник.**https://docs.oracle.com/javase/tutorial/collections/streams/reduction.html


14.Чем метод reduce отличается от метода collect в контексте лямбда-выражений?  
**Ответ.**В отличие от метода reduce, который всегда создает новое значение при обработке элемента, метод collect изменяет или мутирует существующее значение.  
**Источник.** https://docs.oracle.com/javase/tutorial/collections/streams/reduction.html


15.Укажите, какие преимущества дает использование класса Optional?  
**Ответ.** Optional - новый класс в пакете java.util, является контейнером (оберткой) для значений которая также может безопасно содержать null.

Благодаря опциональным типам можно забыть про проверки на null и NullPointerException.  
**Источник.** https://vertex-academy.com/tutorials/ru/java-8-optional/



16.Выполните вывод каждого элемента коллекции collect с помощью метода forEach (), применяя:
итератор
поток  
**Ответ.** 
```java
//итератор
for(Person collect: collect){
System.out.println(collect);
}
//поток
collect.stream().forEach(System.out::println);
```

17.Выполните вывод каждого элемента Map collect с помощью java 8.  
**Ответ.**
collect.entrySet().stream().forEach(System.out::println);

18.Допишите сортировку коллекции users по имени с помощью метода getName() и вывод всех элементов коллекции в консоль (класс User приводить не обязательно).
```java
public class Main {
    public static void main(String[] args) {
        List<User> users = new ArrayList<>();
            users.add(new User("Nick", "Boll"));
            users.add(new User("Jan", "Nicky"));
            users.add(new User("Bot", "Smart"));
users.stream().sorted(Comparator.comparing(o->o.getName());
    }
}
```

19.Допишите код, чтобы вывести только четные элементы коллекции, используя метод filter().
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
        numbers.stream().filter(x->x%2==0).forEach(System.out::println);
        
    }
}
```

20.Допишите код, чтобы вывести количество элементов коллекции, длина которых больше 4, используя методы filter() и count().
```java
public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("John", "Jan", "Tirion", "Marry", "Nikolas");
        System.out.println( names.stream().filter(x->x.getBytes().length==4).count());
    }
}
```

21.Допишите код, чтобы вывести каждый элемент коллекции, умножив его на 2, используя метод map().
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 3, 5, 7);
        numbers.stream().map((s)->s.intValue()*2).forEach(System.out::print);
    }
}
```

22.Создайте новую коллекцию ArrayList и выведите в консоль список четных чисел из коллекции numbers с использованием методов filter() и collect().
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
        List<Integer> evenNumbers =List<Integer> evenNumbers = numbers.stream().filter(x->x%2==0).collect(Collectors.toList());
	        evenNumbers.stream().forEach(System.out::println);
    }
}
```

23.Создайте новую коллекцию LinkedList (имплементация Queue) и выведите в консоль НЕ пустые строки из коллекции ArrayList names с использованием методов filter() и collect().
```java
public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Jaime", "Daenerys", "", "Tyrion", "");
        Queue<String> queue = names.stream().filter(x->!x.isEmpty()).collect(Collectors.toCollection(LinkedList::new));
        queue.stream().forEach(System.out::println);
    }
}
```

24.Выведите имена домашних животных, объединив их в новую коллекцию List<String> petNames из коллекции их хозяев humans, у которых имена домашних животных являются полями класса (в виде отдельных коллекций), используя метод flatMap().
```java
public class Main {
    public static void main(String[] args) {
        List<Human> humans = asList(
            new Human("Sam", asList("Buddy", "Lucy")),
            new Human("Bob", asList("Frankie", "Rosie")),
            new Human("Marta", asList("Simba", "Tilly")));
      List<String> petNames = humans.stream().flatMap(p->(p.getPets()).stream()).collect(Collectors.toList());
		 petNames.stream().forEach(System.out::println);
    }
}
```

25.Найдите и выведите первое по счету число, которое больше 10, используя методы filter() и findFirst().
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 5, 8, 10, 12, 15);
        Optional<Integer> first = numbers.stream().filter(x->x.intValue()>10).findFirst();
        first.stream().forEach(System.out::println);
    }
}
```

26.Найдите и выведите первую попавшуюся фразу (с учетом возможного многопоточного процесса), которая содержит фрагмент "Java", используя методы filter() и findAny().
```java
public class Main {
    public static void main(String[] args) {
        List<String> strings = Arrays.asList("Java is the best", "Java 8", "Java 9", "Jacoco");
         Optional<String> java =strings.stream().filter(x->x.contains("Java")).findAny();
        java.stream().forEach(System.out::println);
     }
}
```

27.Выведите boolean, имеется ли в коллекции хотя бы одно четное значение, используя метод anyMatch().
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 4, 5, 7);
        boolean match = numbers.stream().anyMatch(x->x%2==0);
        System.out.println(match);
     }
}
```

28.Выведите boolean, являются ли все числа коллекции положительным, используя метод allMatch().
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        boolean match = numbers.stream().allMatch(x->x.intValue()>0);
        System.out.println(match);
     }
}
```

29.Выведите boolean, НЕ являются ли все числа коллекции четными, используя метод noneMatch().
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 3, 5, 7, 9);
         boolean match = numbers.stream().noneMatch(x->x%2==0);
	        System.out.println(match);
     }
}
```

30.Какие из ниже приведенных ламбда-выражений не скомпилируется и почему?
1)(int x, int y) -> x+y  
2)(x, y) -> x+y          
3)(x, int y) -> x+y   
4)(x, final y) -> x+y 
5)int x -> x;
6)x -> y -> x + y;
7)x -> (final int y) -> y + x;
8)x -> x -> 5;


31.Скомпилируется ли следующий код и почему?
for (byte b : "Java".getBytes()) {
            foo(() -> b);
 }  
 **Ответ.** Такой код не скомпелируется.


32.Дана матрица 3х3 используя Java 8 преобразуйте ее в одномерный массив.
```java
int[][] matrix = {   {1, 2, 3}
                           , {4, 5, 6}
                           , {7, 8, 9}};
int[] array =Arrays.stream(matrix)
        .flatMapToInt(Arrays::stream) //преобразовываем IntStream<int[]> в IntStream
        .toArray(); // преобразовываем IntStream в int[]

System.out.println(Arrays.toString(array));
```
33.Даны классы:
```java
class BlogPost {
    String title;
    String author;
    BlogPostType type;
    int likes; 
}
enum BlogPostType {
    NEWS,
    REVIEW,
    GUIDE
}
List<BlogPost> posts = Arrays.asList( ... );
```
Определите:
Все уникальные статьи относящиеся к каждому типу статей.
Для каждого типа статьи определите статью с максимальным количеством лайков.
Все статьи относящиеся к каждому типу статей, список статей должен представлять собой строку формата: “Post titles: [title1, title2, …..] “


34.Приведите два способа получения последнего элемента в потоке, в чем особенности вычисления этого значения в потоках.  
**Ответ.**
1) Stream<T> stream = ...; // sequential or parallel stream
Optional<T> last = stream.reduce((first, second) -> second);
Эта реализация работает для всех упорядоченных потоков (включая потоки, созданные из Списки). Для потоков unordered по очевидным причинам неизвестен, какой элемент будет возвращен.
2)CArea last = data.careas.stream()
    .filter(c -> c.bbox.orientationHorizontal)
    .max((e1, e2) -> data.careas.indexOf(e1) - data.careas.indexOf(e2)).get();  
**Источник.** https://overcoder.net/q/79108/%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B8%D1%82%D1%8C-%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BD%D0%B8%D0%B9-%D1%8D%D0%BB%D0%B5%D0%BC%D0%B5%D0%BD%D1%82-stream-list-%D0%B2-%D0%BE%D0%B4%D0%BD%D1%83-%D1%81%D1%82%D1%80%D0%BE%D0%BA%D1%83    


35.Дан код, можно ли его как-то отрефакторить? Если да, то сделайте это.
Подсказка:
Добавьте в список элемент с автором, которые уже есть в списке и проверьте приложение 
books.add(new Book("Java: A Beginner's Guide", "Herbert Schildt"));
```java
class Book {
private String name;
private String author;

// getters and setters
…
}

List<Book> books = new ArrayList<>();

books.add(new Book("Effective Java", "Joshua Bloch"));
books.add(new Book("Thinking in Java", "Bruce Eckel"));
books.add(new Book("Java: The Complete Reference", "Herbert Schildt"));

Map<String, String> bookMap = books.stream().collect(
Collectors.toMap(Book::getAuthor, Book::getName));
bookMap.forEach((author, book) -> 
System.out.println("Author: " + author + " Books: " + book));
```  
**Ответ.** В первом случае код сработает. Во втором случае,при добавление в коллекцию книги с уже имеющимся автором,
будет сгенерирована ошибка java.lang.IllegalStateException, т.к. такой ключ уже существует.Т.е. в коллекции Map не может быть 2 
одинаковых ключа.

36.Дан код
```java
class Employee {
    Integer employeeId;
    String employeeName;
 
    // getters and setters
}
 
class Department {
    Integer employeeId;
    String department;
 
    // getters and setters
}

public class Main {
    public static void main(String[] args) {
        List<Employee> employees = new ArrayList<>();
        List<Department> departments = new ArrayList<>();

        populate(employees, departments);

       List<Employee> salesEmployees = ...
    }
}
```
Замените многоточие, чтобы определить сотрудников находящихся в отделе “sales”


37.Дан код
```java
class Tuple<T1, T2> {
    private T1 item1;
    private T2 item2;
    // getters and setters
}
List<String> names = new ArrayList<>(Arrays.asList("John", "Jane", "Jack", "Dennis")); 
List<Integer> ages = new ArrayList<>(Arrays.asList(24, 25, 27));
List<Tuple<String, Integer>> namesAndAges = … 
```
Выполните операцию ‘zip’ для коллекций ages и names.
Zip: операция «zip» немного отличается от стандартной «concat» или «merge». В то время как операции «concat» или «merge» просто добавят новую коллекцию в конец существующей коллекции, операция «zip» возьмет элемент из каждой коллекции и объединит их.
Например, в результате выполнения этого задания должна получиться коллекция:
[John;24, Jane;25, Jack;27]


38.Дан код, замените  {code} и {type} так, чтобы получить нужные результаты
Collection<String> strings = Arrays.asList("a1", "b2", "c3", "a1");
// Удалить все дубликаты
List<String> unique= strings.stream().{code}
// напечатает unique= [a1, b2, c3]
System.out.println("unique = " + unique); 
// Объединить все элементы в одну строку через разделитель : и обернуть тегами <b> ... </b>
String join = strings.stream().collect({code});
// напечатает <b> a1 : b2 : c3 : a1 </b>
System.out.println("join = " + join); 
// Преобразовать в map, сгруппировав по первому символу строки
Map<String, List<String>> groups = strings.stream().collect({code});
// напечатает groups = {a=[a1, a1], b=[b2], c=[c3]}
System.out.println("groups = " + groups); 
// Преобразовать в map, сгруппировав по первому символу строки и в качестве значения взять второй символ, если ключ повторяется, то значения объединить через “:” 
Map<String, String> groupJoin = strings.stream()
     .collect(Collectors.groupingBy({code}));
// напечатает groupJoin = groupJoin = {a=1:1, b=2, c=3}
System.out.println("groupJoin = " + groupJoin);

Collection<Integer> numbers = Arrays.asList(1, 2, 3, 4);
// Получить сумму нечетных чисел
{type} sumOdd = numbers.stream().collect({code});
// напечатает sumEven = 4
System.out.println("sumOdd = " + sumOdd); 
 // Вычесть из каждого элемента 1 и получить среднее
 double average = numbers.stream().collect({code});
 // напечатает average = 1.5
System.out.println("average = " + average); 
// Прибавить к числам 3 и получить статистику: количество элементов, их сумму, макс и мин. значения, а также их среднее.
{type} statistics = numbers.stream().collect({code});
// напечатает statistics = … {count=4, sum=22, min=4, average=5.500000, max=7}
System.out.println("statistics = " + statistics);
// Разделить числа на четные и нечетные
Map<Boolean, List<Integer>> parts = numbers.stream().collect({code});
// напечатает parts = {false=[1, 3], true=[2, 4]}
System.out.println("parts = " + parts); 



39.Дан поток, определите количество вхождений каждого из символов, составляющих поток.
Stream<String> words = Stream.of("Java", "Magazine", "is", "the", "best");


40.Дан код, как он будет выглядеть если modem обернуть в Optional?
```java
   boolean isInRange = false;
    if (modem != null && modem.getPrice() != null
      && (modem.getPrice() >= 10
        && modem.getPrice() <= 15)) { 
        isInRange = true;
    }
    return isInRange;
```

41.Дан код, замените {code}, чтобы получить первый объект, которые не null, если такого нет вернуть “default’
```java
private Optional<String> getEmpty() {
    return Optional.empty();
}
 
private Optional<String> getHello() {
    return Optional.of("hello");
}
 
private Optional<String> getBye() {
    return Optional.of("bye");
}
String firstNonNull = Stream.of(getEmpty(), getHello(), getBye()).{code};
```


