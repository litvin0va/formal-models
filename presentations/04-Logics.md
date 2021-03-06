# Математические модели вычислений

## Тезис Чёрча-Тьюринга. Теорема Райса о неразрешимости нетривиальных свойств.

## Формальные системы. Полнота и непротиворечивость. Теоремы Гёделя о неполноте. 

## Теоретико-модельные и теоретико-доказательные подходы к верификации.

maxim.krivchikov@gmail.com

Материалы курса: https://maxxk.github.io/formal-models/


# Тезис Чёрча-Тьюринга
Исходная задача для Entscheidungsproblem — получить строгое понятие алгоритма (вычислимой функции). Под вычислимой понимается функция, значение которой для некоторого заданного аргумента может получить человек с использованием алгоритма (последовательности шагов с условиями).

**Определение** *(Тезис Чёрча-Тьюринга).* Вычислимые функции — это функции, которые можно вычислить с использованием машины Тьюринга или другой эквивалентной модели.

## «Определение» понятия программы
Программой, решающей определённую задачу, назовём код машины Тьюринга, которая реализует решение задачи, в терминах некоторой универсальной машины Тьюринга, или эквивалентной ей модели вычислений.

# Относительная сложность математических проблем
По следующей ссылке: http://www.scottaaronson.com/blog/?p=2725
представлены результаты работы (в том числе — препринт статьи, исходный код, видеолекция и т.д.), авторы и последователи которой построили с помощью компилятора/интерпретатора с языка программирования относительно высокого уровня в машину Тьюринга, следующие машины на двоичном алфавите:

- машина из 4888 состояний, которая останавливается в том и только в том случае, когда существует контрпример к гипотезе Гольдбаха
- машина из 744 состояний, которая останавливается в том и только в том случае, когда существует контрпример к гипотезе Римана
- машина из 1919 состояний, которая останавливается в том и только в том случае, если найдена противоречивая формула, выводимая в ZFC (т.е. машина, останов которой в недоказуем в ZFC) 

# Теорема Райса о неразрешимости нетривиальных свойств частичных функций
*Исходная формулировка — в терминах частично-рекурсивных функций Клини — другой универсальной модели вычислений, эквивалентной машине Тьюринга.*
Для любого нетривиального свойства частичных функций не существует общего эффективного метода разрешения того, вычисляет ли данный алгоритм частичную функцию с таким свойством.
Тривиальные свойства — свойства, которые выполняются для всех вычислимых функций (или не выполняются ни для одной).

Частичная функция из *X* в *Y* — функция, область определения которой не совпадает со всем *X*. Вычислимые функции частичны, т.к. можно представить машину Тьюринга, которая останавливается для некоторых входных значений и не останавливается для других.

В терминах «программ» универсального вычислителя: для любого нетривиального *семантического* свойства программ не существует общего эффективного метода разрешения того, обладает ли данная программа таким свойством.

# Теорема Райса
## Следствие для практики
Невозможно создать алгоритм, который определяет, обладает ли произвольная программа некоторым нетривиальным свойством.

⇒ невозожна автоматическая формальная верификация

## В терминах распознающих машин Тьюринга
Пусть *S* — нетривиальное множество языков, т.е. существуют две машины Тьюринга — распознающая, что язык находится в *S* и распознающая, что язык не находится в *S*. Тогда для произвольной данной машины Тьюринга вопрос о том, принадлежит ли распознаваемый ей язык *S* является неразрешимым.

# Теорема Райса
## Схема доказательства
Сводим утверждение теоремы к проблеме останова. Пусть:
- *a* — строка-программа
- *a ↦ 𝐅~a~* — частичная функция, соответствующая программе *a*
- *a ↦ P(a)* — данный алгоритм, разрешающий некоторое нетривиальное свойство
- *n* — строка-программа, которая не завершается ни для какого входа (бесконечный цикл)
- без ограничения общности, *P(n) = 0*
- *b* — строка-программа, для которой *P(b) = 1* (по условию нетривиальности свойства)

Покажем, что из этих элементов можно создать алгоритм *H(a, i)*, решающий проблему останова для программы *a* на входе *i*.
Построим *t* — строку-программу, которая для входа *j* выполняет вычисление *𝐅~a(i)~,* затем — *𝐅~b(j)~* и возвращает последний результат.

Тогда *P(t)* решает проблему останова.

# Теорема Райса
## Пояснение
Теорема существенно опирается на тот факт, что мы отождествляем все программы, которые реализуют одну и ту же функцию, т.е. рассматриваем семантику программы, игнорируя её синтаксис. Такое отождествление называется «функциональная экстензиональность».

 *P(t)* решает проблему останова, т.к.:
1. Если *a* завершается на *i*, то 𝐅~t~ = 𝐅~b~ и *H(a, i)* = 1
2. Если *a* не завершается на *i*, то  𝐅~t~ = 𝐅~n~ (никогда не завершается) и *H(a, i)* = 0

# Программа Гильберта
Искомые свойства формальной системы для оснований математики:
1. Полнота (мы можем переписыванием получить из аксиом все истинные утверждения математики)
2. Непротиворечивость (мы не можем получить переписыванием из аксиом ложное утверждение)
3. Разрешимость (руководствуясь простым набором правил можно для любой формулы получить, выводима она или нет).

# Формальная система
— конструкция, отражающая концепцию формализма: теории представляются в виде формул, которые можно менять по заданным правилам
Составные части:
1. Конечный *алфавит*, из символов которого составляются *формулы* — строки.
2. *Грамматика* — набор правил, описывающий как составить корректно сформированные формулы (*well-formed formulas*, **wf**). Часто под грамматикой подразумевается процедура разрешения, является ли формула корректно сформированной.
3. *Схемы аксиом* — набор корректно сформированных формул (или схем формул — формул с «метапеременными», вместо которых можно подставлять произвольные формулы).
4. *Правила вывода* — правила, по которым из нескольких корректно сформированных формул, удовлетворяющих некоторой схеме, можно получить новую корректно сформированную формулу.

# Пример: исчисление высказываний
1. Алфавит:
    - *переменные* (*a, b, c, …, a~1~, b~1~, c~1~, …*)
    - *логические операторы* (¬, ∧, ∨, ⊕, →, ↔)
    - *технические символы* (скобки — (), [])
2. Грамматика: переменная **wf**; формула в скобках **wf**;

отрицание — унарный префиксный оператор с высшим приоритетом связывания; 

остальные — бинарные операторы,

приоритет и ассоциативность других операторов не определены, если не указано обратное (нужно всё брать в скобки — но вообще проще предполагать, что правила работают с синтаксическими деревьями)

# Исчисление высказываний
3. Аксиомы (11 схем аксиом, далее ссылаемся с префиксом A):

Импликация:

a.  *A → (B → A)* — абстракция,
b.  *(A → (B → C)) → ((A → B) → (A → C))* — композиция,

Конъюнкция:

c.  *(A ∧ B) → A* — выделение формулы слева,
d.  *(A ∧ B) → B* — выделение формулы справа,
e.  *[A → B] → [(A → C) → (A → (B ∧ C))]* — конструктор конъюнкции,

Дизъюнкция:

f.  *A → (A ∨ B)* — конструктор дизъюнкции слева,
g.  *B → (A ∨ B)* — конструктор дизъюнкции справа,
h.  *[A → C] → [(B → C) → ((A ∨ B) → C)]* — разбор случаев,

Отрицание:

i.  *(A → B) ⟶ (¬B → ¬A)* — контрапозитивное высказывание,
j.  *A → ¬¬A*
k. *¬¬A → A* (аксиома двойного отрицания, double negation) или *A ∨ ¬A* (закон исключённого третьего, law of excluded middle, LEM)

# Исчисление высказываний
4. Правило вывода (*modus ponens*, дословно «правило вывода», MP)

Для краткости правила вывода и вообще отношение выводимости записывают с помощью символа ⊦.

*P, P → Q ⊦ Q* — «применение функции»

Нас интересуют общезначимые формулы исчисления высказываний — формулы, истинные при любых наборах переменных.

**Определение.** Формула *выводима*, если её можно построить из аксиом и правил вывода. *Вывод* — конечная последовательность формул, каждый из элементов которой является аксиомой, либо получается применением правила вывода к нескольким из предыдущих формул.

# Исчисление высказываний
<style>table td { padding-right: 2em; }</style>
**Пример.** *A → A* выводима. Приведём вывод (ссылаемся на предыдущие с префиксом F):

-------------------------------------------------------   ------------------------------
1. *(A → ((A → A) → A)) → ((A → (A → A)) → (A → A))*      [A-b: A,C := A; B := (A → A)]
2. *A → ((A → A) → A)*                                    [A-a: A := A, B := (A → A)]
3. *(A → (A → A)) → (A → A)*                              [MP: P:= F2; (P → Q) := F1]
4. *A → (A → A)*                                          [A-a: A, B := A]
5. *A → A*                                                [MP: P := F4, (P → Q) := F3]
-------------------------------------------------------   ------------------------------
 
**Замечание.** Использовались только аксиомы группы импликации и правило MP, в котором тоже фигурирует только оператор импликации.

# Интерпретация формальной системы
 — множество допустимых значений переменных и способ перевода синтаксически корректных формул системы в функции на этом множестве.

Обычно интерпретация определяет истинность формул системы в виде соответствия:
*(формула, значения всех переменных) → { истина, ложь }*

## Модель формальной системы 
— интерпретация, в которой все аксиомы общезначимы.

Если выводимая формула верна во всех моделях — она общезначима.
Если выводимая формула неверна во всех моделях — система противоречива.
Если формула верна не во всех моделях, она невыводима и является независимой от системы аксиом.

Пример относительно простого исследования аксиоматики ZFC на предмет независимости аксиом: http://projecteuclid.org/euclid.ndjfl/1093888220  

Более подробно про формальные системы можно почитать здесь: http://lpcs.math.msu.su/~zolin/ax/pdf/2015_Axiomatic_method_Zolin_Lectures.pdf 

# Исчисление высказываний: основные свойства

Стандартная модель — алгебра логики (булева алгебра).

**Теорема.** Любая выводимая формула исчисления высказываний общезначима.

**Определение.** Исчисление *непротиворечиво*, если не существует **wf** выводимой формулы, для которой выводимо её отрицание.

**Следствие.** (о непротиворечивости исчисления высказываний) Исчисление высказываний непротиворечиво.

**Определение.** Исчисление *полно*, если в нём выводимы все истинные формулы.

**Теорема.** Исчисление высказываний полно — все общезначимые формулы в нём выводимы.

**Определение.** Система аксиом *независима*, если в ней нет аксиом, которые можно вывести из других входящих в систему.

# Пример: исчисление предикатов
## логика первого порядка
1. Алфавит — логические и не логические символы
    - логические: квантификаторы ∀, ∃; связки (→, ¬, возможно, дополнительные); технические знаки (скобки, пунктуация), переменные, символ равенства
    - не логические: *n*-арные предикатные символы  функциональные символы
        - предикат это «высказывание об объектах», функция — «преобразование объектов»

2. Синтаксис: термы и формулы
    - термы — переменные или функции от термов со всеми аргументами
    - формулы — как в исчислении высказываний, а также:
        - предикатные символы от термов со всеми заданными аргументами
        - квантификаторы, связывающие переменную (∀x P(f(x)), ∃y Q(g(y)))

# Логика первого порядка
3. Аксиомы
    1. Все аксиомы исчисления высказываний.
    4. ∀x.A(x) → A(y)
    5. A(x) → ∃y.A(y)
    6. Дополнительные аксиомы для предикатных и функциональных символов.

4. Правила вывода
    1. A → B, A ⊦ B
    2. B → A(x) ⊦ B → ∀x.A(x), где *x* — не свободная переменная *B*
    3. A(x) → B ⊦ ∃x.A(x) → B, где *x* — не свободная переменная *B*
    4. Переименование переменных. 

# Арифметика Робинсона
Логика первого порядка над следующей сигнатурой:

- 0-местный функциональный символ *0*,
- 1-местный функциональный символ ' («следующее натуральное число», x' = x+1),
- 2-местные символы = (предикатный) и +, × (функциональные).

Аксиомы:

- ¬(0 = x') — 0 не равен x+1
- x' = y' → x = y — равенство ненулевых значений
- ¬(x = 0) → ∃y(x = y') — ненулевое значение следует за некоторым значением
- x + 0 = x — 0 нейтрален по сложению
- x + y' = (x + y)' 
- x × 0 = 0
- x × y' = (x × y) + x — дистрибутивность умножения   


# Первая теорема Гёделя о неполноте
Если формальная система достаточно выразительна для описания элементарной арифметики, она не может быть одновременно непротиворечива и полна. Для непротиворечивой теории существуют утверждения (формулы), которые не могут быть ни выведены, ни опровергнуты. 

Основная идея: достаточно выразительная формальная система не может быть одновременно полна и непротиворечива.

В настоящем курсе мы рассмотрим простую схему доказательства более слабой теоремы, которая соответствует этой идее. А именно:

Формальная система, *достаточно выразительная для описания утверждений о машинах Тьюринга,* не может быть одновременно непротиворечива и полна.


# Схема простого доказательства аналога теоремы Гёделя о неполноте

Предположим, что существует полная и непротиворечивая *рекурсивно аксиоматизируемая* формальная система F, в которой представимы утверждения о машинах Тьюринга. Тогда с помощью этой системы проблема останова разрешима следующим образом.

Пусть дана машина M, про которую нужно определить, останавливается ли она на пустой ленте. Это не ограничивает общность: для любой машины с входными данными мы можем подставить эти входные данные в код машины.

Начнём перечисление всех выводов, допустимых в теории F. Для каждого из них проверяем, является ли он доказательством утверждения «M останавливается на пустой ленте» или доказательством утверждения «M не останавливается на пустой ленте».

Т.к. F полна, рано или мы найдём одно из доказательств. Т.к. F непротиворечива, оно будет корректным.

Таким образом, мы построили процедуру разрешения неразрешимой проблемы останова, следовательно, система F из нашего предположения не может существовать.

# Доказательство Хайтина с использованием Колмогоровской сложности
Используется парадокс Берри: определение "наименьшее положительное число, которое нельзя определить восемью словами" определет такое число восемью словами (на русском языке).

## Колмогоровская сложность
Зафиксируем некоторый язык программирования (C, LISP, код универсальной машины Тьюринга и т.п.).

Колмогоровская сложность целого числа x (K(x)) — минимальная длина программы (в битах) на выбранном языке программирования, которая выводит x и останавливается.

# Доказательство Хайтина
Утверждение теоремы: для любой достаточно выразительной формальной теории существует такое число L (зависит от теории и языка программирования), такое, что для любого числа x утверждение K(x) > L не может быть доказано в этой теории.

<!--
Пусть заданы язык программирования и непротиворечивая формальная теория S, для которой мы можем:
- написать программу, перечисляющую все доказательства ℕ → proof
- написать программу, проверяющую, что доказательство доказывает некоторое утверждение
-->

Пусть для любого L есть такое число z, что существует формальное доказательство "K(z) > L". Пусть w — первое по лексикографическому порядку доказательство этого утверждения. Возможно написать программу P, которая перебором доказательств находит для данного L такое число z. Тогда длина программы — |P| = C + log~2~ L. Тогда для достаточно большого L, |P| < L. Тогда K(z) = |P| < L. 

Программ длины не более L битов — не более 2^L+1^, следовательно, существует хотя бы одно 0 ≤ x ≤ 2^L+1^, такое, что K(x) > L. 

# Вторая теорема Гёделя о неполноте

Если в формальной системе можно представлять утверждения об арифметике и о формальной доказуемости, и если такая система включает формулу, представляющую непротиворечивость этой системы, то такая система противоречива.

(непротиворечивость формальной системы нельзя показать внутри самой этой системы)

# Схема доказательства аналога второй теоремы Гёделя о неполноте с помощью Колмогоровской сложности
Парадокс "неожиданной контрольной": преподаватель объявляет классу "на следующей неделе будет контрольная, но вы не можете узнать заранее, в какой день она будет".

Пусть L — число из предыдущего доказательства для заданной формальной системы. Пусть m — количество целых чисел 0 ≤ x ≤ 2^L+1^, таких, что K(x) > L. m ≥ 1. 

Пусть m = 1. Тогда существует единственное x: K(x) > L, а все остальные числа в интервале имеют сложность < L. Тогда можно построить формальное доказательство того, что K(x) > L, путём перебора всех формальных доказательств K(y) ≤ L, пока не найдём 2^L+1^ таких y; оставшееся — это x.

Существование формального доказательства противоречит определению L, поэтому если система F непротиворечива, m ≥ 2.

# Схема доказательства аналога второй теоремы Гёделя о неполноте
Если система F непротиворечива, m ≥ 2. В достаточно выразительной теории можно записать и доказать это необходимое условие. 

Если в системе F можно доказать её непротиворечивость, в ней можно доказать и то, что m ≥ 2.

Далее — аналогичным образом поднимаем оценку снизу на значение m, пока не получим противоречие.




# Теоремы Гёделя о неполноте
Схемы классических доказательств теорем Гёделя о неполноте.
http://plato.stanford.edu/entries/goedel-incompleteness/

Доказательства с помощью сведения к проблеме останова, использованные в презентации: http://www.scottaaronson.com/blog/?p=710

Доказательство первой теоремы Гёделя с использованием понятий функционального программирования (А.М. Миронов, МаТИС): http://intsysjournal.org/articles/is04/17_mironov.pdf

# Программа Гильберта
Искомые свойства математики:
1. ~~Полнота (мы можем переписыванием получить из аксиом все истинные утверждения математики)~~
2. ~~Непротиворечивость (мы не можем получить переписыванием из аксиом ложное утверждение)~~
3. ~~Разрешимость (руководствуясь простым набором правил можно для любой формулы получить, выводима она или нет).~~

## Но не всё потеряно

# Теория моделей и теория доказательств
Теория моделей — изучает связь синтаксиса (формальных систем) и семантики (моделей для таких систем)

Теоретико-модельные подходы к формальной верификации: программа представляется в виде некоторой модели, допускающей исчерпывающую проверку интересующих свойств (enumerative and symbolic model checking). Обычно — автоматные модели, а также методы абстрактной интерпретации (символьные вычисления и т.п.).

Теория доказательств — изучает структуру формальных доказательств

Дедуктивные (теоретико-доказательные) подходы к формальной верификации — программа и свойства записываются в виде формул в формальной системе, доказательства строятся как вывод в формальной системе.

<!-- Next time

# Логика второго порядка
— допускается квантификация по отношениям. 
# Естественная дедукция

# Системы переписывания термов и правила редукции

# Конфлюэнтность

# Теорема Чёрча-Россера

# Параллельные редукции

# Свойство нормализации

# Свойство сильной нормализации

# Вычисления за пределами тезиса Чёрча-Тьюринга
-->

# Задачи


**Задача 4.1. \*\*\***
~ Сформулировать проблему останова в виде формулы логики первого порядка над арифметикой Робинсона.

**Задача 4.2. (5\* / корень из числа соавторов)** 
~ По следующей ссылке приведено средство для разработки визуализаторов логического вывода: http://www.is.ocha.ac.jp/~asai/MikiBeta/
Необходимо повторить этот результат — разработать средство для достаточно простого создания визуализаторов логического вывода как минимум систем первого порядка на HTML5/CSS/JavaScript (желательно — опубликовать в OpenSource, как пример эмулятора машины Тьюринга с предыдущего занятия).

**Задача 4.3 (5\*)**
~ Закодировать проверку нетривиального математического утверждения машиной Тьюринга с использованием методов, представленных в http://www.scottaaronson.com/blog/?p=2725
