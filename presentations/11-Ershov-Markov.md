# Математические модели вычислений

## Операторные схемы программ
## Схемы Янова
## Нормальные алгорифмы Маркова
## Язык программирования Рефал

maxim.krivchikov@gmail.com

https://maxxk.github.io/formal-models/

# Операторная схема программы
Классический советский подход к теории программирования, предложенный А.А. Ляпуновым в первом курсе «Принципы программирования», который он читал в 1952/53 году на кафедре вычислительной математики.

В более позднем определении А.П. Ершова:

Задано конечное множество *операторов* F = { F~1~, …, F~n~}. Входы и выходы описываются в терминах *полюсов* операторов P = A ∪ R — объединение непересекающихся множеств *аргументов* A = {a~1~, …, a~p~} и *результатов* R = { r~1~, …, r~q~ }. *Распределение полюсов* — отображение V : P → F.

*Граф переходов* — ориентированный граф C = (F, J), где J — бинарное отношение, задающее для оператора его преемников по передаче управления.
Компоненты связности графа переходов — отдельные программы в программном комплексе.

*Скелет* программы — набор перечисленных множеств S = (F, C, A, R, V).

*Память* описывается множеством X = { x~1~, …, x~m~ } и распределяется среди полюсов отображением L : P → X.

Операторная схема программы — набор G = (S, X, L).

# Задача экономии памяти

А.П. Ершов в книге (список литературы на последних слайдах) рассматривает задачу экономии памяти: каким образом можно использовать минимальное множество памяти X, сохраняя семантику программы?

Постановка задачи: по заданной схеме программы с *распределением памяти* L построить новое распределение памяти L', использующее, по возможности, память меньшего объёма.

*Информационный граф* I = (P, M) — двудольный граф M ⊂ R×A, который сопоставляет результаты оператора с аргументами его преемников. *Маршрут информационной связи* — путь в информационном графе, задаётся первым результатом и последним аргументом.

Компоненты связности информационного графа называются *областями действия*.

Области действия *несовместимы* тогда и только тогда, когда в каждой из них найдутся результаты r и r', соответственно, такие, что:

  * V(r) = V(r') или
  * V(r) — внутренний оператор маршрута информационной связи (r', a')
  * V(r') — внутренний оператор маршрута информационной связи (r, a)

Задача экономии памяти решается выделением несовместимых областей действия раскраской графа и объединением совместимых областей действия.  

# Схема Янова
Модификация операторной схемы программ.
Область приложения — исследование способов задания условий в программе и эквивалентных преобразований программ с условиями.

Не рассматривается понятие памяти и распределения памяти. Все операторы одноместны, принимают на вход исходное состояние памяти и возвращают полностью изменённое состояние. 

Вводятся счётные множества *предикатных символов* **P** = { p~1~, p~2~, … } и *операторных символов* **A** = { A~1~, A~2~, … }.  

*Оператор* A = A(P) — пара из операторного символа A и некоторого (возможно, пустого) множества предикатных символов P, которое называется *сдвигом* оператора A.

# Схема Янова
*Граф переходов* — ориентированный граф, множество вершин которого состоит из неотрицательного числа *преобразователей*, *распознавателей* и одного *останова*. Из преобразователя выходит в точности одна дуга, из распознавателя — две различные (*плюс-стрелка* и *минус-стрелка*). Выделяется одна *входная* вершина графа и помечается *входной стрелкой*.

*Преобразователи* помечены операторными символами, *распознаватели* помечены логическими формулами над *предикатными* символами.

*Схема Янова* G(p~1~, …, p~k~) 

# Схема Янова
![](http://pco.iis.nsk.su/wiki/images/8/80/Yanov_schemata.gif)

# Семантика схемы Янова
Для того, чтобы схема задавала программу, необходимо дать *интерпретацию* операторным и предикатным символам, и описать алгоритм выполнения интерпретированной схемы.

Дано некоторое множество *состояний памяти* D. 
Предикатные символы p~i~ соответствуют предикатам π~i~ : D → { **f**, **t** }. Сами p~i~ в программе назовём *предикатными переменными*. 

Операторным символам A~j~ сопоставляются (возможно, частичные) функции φ~j~ : D → D

# Выполнение схемы Янова

**Начальный шаг.** Берём произвольное d ∈ D в качестве исходного состояния памти и присваиваем значения всем предикатным переменным p~i~ ≡ π~i~(d). Передаём управление на входную вершину графа переходов. 

**Шаг выполнения.** Пусть d — текущее состояние памяти, Δ = (σ~1~, …, σ~k~) — текущие значения предикатных переменных, S — текущая вершина графа переходов.

1. Если S — останов, то выполнение завершается, и d является результатом выполнения схемы в данной интерпретации.
2. Если S — распознаватель с условием F(p~1~, …, p~k~). Вычисляем σ = F(Δ) и передаём управление по плюс-стрелке, если σ=**t** и по минус-стрелке, если σ=**f**.
3. Если S — преобразователь A~j~(P~j~), вычисляем новое состояние памяти d' = φ~j~(d) и значения предикатных переменных в  сдвиге P~j~ : p~i~ ≡ π~i~(d'). Управление передаётся на следующую вершину графа.

Таким образом, получена частичная функция d = **F**~G,I~(d~0~).

# Эквивалентность схем
Схемы G~1~ и G~2~ *сравнимы*, если они заданы над одним и тем же множеством предикатных символов, а также у одинаковых операторов совпадают сдвиги.

Две сравнимые схемы *эквивалентны* в некоторой совместной интерпретации I, если F~G1,I~(d) = F~G2,I~(d).

Две сравнимые схемы *функционально эквивалентны*, если они эквивалентны в любой совместной интерпретации.

*Операционная история* (след) интерпретированной схемы Янова H~G,I~(d) — полная последовательность выполняемых операторов и наборов значений функциональных переменных. Для исключения циклов вершины графа помечаются наборами значений предикатных переменных. Если при выполнении мы попали в вершину, помеченную таким же набором значений, что и текущий набор Δ, считаем, что мы попали в бесконечный цикл.

Две сравнимые схемы *операционно эквивалентны*, если они одинаково работают в любой совместной интерпретации, т.е. 
H~G1,I~(d) = H~G2,I~(d).

**Теорема.** Функциональная эквивалентность равносильна операционной эквивалентности.
 
# Эквивалентность схем
*Конфигурации* схемы k ∈ K(G) строятся аналогично операционным историям, но без заданной интерпретации индуктивно:

**Начальный шаг.** Выберем произвольный набор исходных значений предикатных переменных Δ. 
**Очередной шаг.** Текущий набор Δ, текущая вершина S. Уже обработанные вершины помечены.

1. Если S — помеченный распознаватель, то мы попали в пустой цикл и конфигурация не может быть построена.
2. Если S — непомеченный распознаватель с условием F, помечаем его, вычисляем F(Δ) и переходим к вершине-преемнику.
3. Если S — останов, построение конфигурации завершено.
4. Если S — оператор, то записываем A~i~ в конфигурацию, и в качестве нового значения Δ' помещаем произвольный набор, образующий с набором Δ допустимую пару для оператора A~i~.

Две сравнимые схемы *формально эквивалентны*, если их множества их конфигураций совпадают.

**Теорема.** Функциональная эквивалентность равносильна формальной эквивалентности. 

# Эквивалентные преобразования
Вводится набор из 13 аксиом и 5 правил вывода, определяющий все примитивные эквивалентные преобразования схем Янова.

**Теорема.** Для любых двух эквивалентных схем Янова можно построить последовательность эквивалентных преобразований, которые приводят их к общему виду.

**Теорема.** Задача эквивалентности двух сравнимых схем Янова разрешима.  

# Алгорифмы Маркова
Пусть задан конечный алфавит **A**, не содержащий символов «перевод строки» (γ), «→» и «→.». Нормальным алгорифмом назовём последовательность *формул подстановки* вида:


< строка **A^\*^** > (образец) → < строка **A^\*^** > (результат)
< строка **A^\*^** > → . (останов) < строка **A^\*^** >

На вход алгорифма подаётся строка **A^\*^**. Далее для каждого правила по порядку выполняется поиск образца в строке слева. 

Если образец найден, т.е. для правила L → D входная строка T представлена в виде T = R · L · S, то подстрока L заменяется на D и результатом шага объявляется строка T' = R · D · S. Если стрелка — стрелка останова, то выполнение завершается с результатом T', в противном случае выполняется следующий шаг (просмотр образцов сначала). 

Если образец не найден, переходим к следующему правилу.

Если ни для одного правила образец не найдет, выполнение завершается с результатом T. 

# Примеры
1. Алгоритм получения модуля унарных чисел N, M. 
На вход подаётся строка N*M, где N и M — унарные числа в алфавите 1.
1 * 1 → *
\* → .

2. Алгоритм поиска наибольшего общего делителя чисел N*M. Пусть a, b, c – служебные символы.
1 a → a 1
1 * 1 → a *
1 * → * b
b → 1
a → c
c → 1
\* → .

Визуализатор:
http://cmcmsu.no-ip.info/1course/alg.schema.nam.htm#


# Рефал
— [РЕкурсивных Функций АЛгоритмический] язык программирования, построенный на основе модели нормальных алгорифмов Маркова.

Функции задаются в терминах правил переписывания входных строк (деревьев) в выходные.
Последовательность правил, разделённых символом `;`. Слева от знака `=` записываются образцы, справа — результаты. После унификации входной строки с образцом выполняется подстановка полученных значений переменных в результат. Вызов функции — в угловых скобках, круглые скобки позволяют задавать и сопоставлять деревья и образцы на деревьях.

Для наглядности знак `=` заменён на →

```
Beta {
   (λ s.var '.'  e.body) t.value e.rest ->
      Step <Subst s.var t.value e.body> e.rest ;
    → Stuck;
}
```

<span class="small">
Турчин В. Ф. «Метаалгоритмический язык». Кибернетика, вып. 4 (1968 г.): 45–54.
</span>

# Рефал

В образцах можно задавать переменные:

* `s.имя-переменной` принимает любой символ, не являющийся скобкой
* `t.имя-переменной` (терм) принимает любой символ, или парные скобки с их содержимым
* `e.имя-переменной` выполняет поиск. На первом шаге `e`-переменная пуста. Если не удалось сопоставить образец, `e`-переменная расширяется на следующий терм.

При успешном сопоставлении с образцом, значения переменных можно использовать при генерации результата.

```
Beta {
   (λ s.var '.'  e.body) t.value e.rest ->
      Step <Subst s.var t.value e.body> e.rest ;
    → Stuck;
}
```


Н.М. Нагорный: алгорифмы Маркова можно эквивалентным образом задавать в виде нескольких конечных наборов правил подстановок [«функций»], бесконечного количества [функций] и бесконечного набора бесконечных функций. 

# Расширения Базового Рефала
Условия: промежуточный результат сопоставляется с образцом (Рефал-5):

```
t.neutral e.rest,
  <Beta e.rest> : s.state e.result =
  s.state t.neutral e.result ;
```

Функции высшего порядка: функции передаются так же, как и данные (Рефал-7):

```
(e.1) e.rest,
  <Beta e.1> : e.betaResult =
  <{
    Step e.result = Step (e.result) e.rest ;
    Stuck e.result,
      <Beta e.rest> : s.state e.result2 =
      s.state (e.result) e.result2 ;
  } e.betaResult>;
```

<span class="small">
Рефал-5: В.Ф. Турчин. «Рефал-5. Руководство по программированию и справочник» http://refal.net/rf5_frm.htm
Рефал-7: С.Ю. Скоробогатов, А. М. Чеповский. «Разработка нового диалекта языка Refal». Информационные технологии, вып. 9 (2006 г.): 31–38.
</span>

# Метавычисления и суперкомпиляция
Метавычисления — это раздел теории и практики программирования, связанный с разработкой и использованием метапрограмм — конструктивных метасистем над программами.^1^

Суперкомпиляция — техника преобразования программ [в первую очередь — оптимизации], основанная на построении полной и самодостаточной модели программы.^2^

Две основные стадии суперкомпиляции:
1. *Прогонка* программы на параметризованных входных данных (частичная специализация). Выполняется построение множетсва конфигураций машины.
2. *Свёртка* результата прогонки для получения остаточной программы (выделение рекурсии).

<span class="small">
^1^ С.М. Абрамов. Основы метавычислений. Курс НОУ ИНТУИТ. http://www.intuit.ru/studies/courses/1067/221/info
^2^ И.Г. Ключников. Суперкомпиляция: идеи и методы. Практика функционального программирования, № 7, 2011.
</span>

# Кибернетические основания математики

# Система типов для языков семейства Рефал
Ограничимся функциями без побочных эффектов. Тип значения — завершимая функция, принимающая или отвергающая значение.

```
Bool = { 0 = ; 1 = ; }
```

Тип функций задаёт допустимый набор типов аргумента и типов выходных значений (разделены знаком `--`) Суждение «функция f обладает типом g» означает, что для любого входного значения, распознаваемого g, f завершится без ошибок, и её возвращаемое значение будет распознано соответствующим типом для g.

```
BoolBinaryOperation = { s.1 s.2, <Bool s.1> <Bool s.2> -- s.3, <Bool s.3> }
BoolIdentity = { s.1, <Bool s.1> -- s.1 }
```

# Суждение типизации
— применение суперкомпиляции к типу и функции на произвольном выражении.

```
BoolBinaryOperation ≡ { t.FN = { s.1 s.2, <Bool s.1> <Bool s.2> : s.1 s.2 = <t.FN s.1 s.2> : s.3, <Bool s.3> = ;
  e.skip = ; } }
<HasType BoolBinaryOperation F> ≡ < Supercompile [<BoolBinaryOperation F> e.1] >
```

Последний образец `e.skip` срабатывает в случае, если входные данные не удовлетворяют условиям типа.
Возможные случаи:
1. Успешная типизация: Суперкомпиляция уничтожает вызов функции t.FN, результат — общезначимый тип `{ e.1 = }`.
2. Ошибка типизации: Суперкомпиляция приходит к возможному контрпримеру `{ … = < > ; … }`
3. Неопределённый результат: Суперкомпиляция не может уничтожить вызов функции и генерирует нетривиальную остаточную программу. `R ≡ { … ; … }`. В этом случае можно предоставить дополнительные данные в исходном определении, или в определении R':

```
<HasType T F> ⟶ R
<HasType T F R'> ⟶ <HasType R' <Supercompile [<T F> e.1]>> <HasType { e.1 = } R'>
```

# Подтипы
Наиболее точный тип можно получить из определения функции.

```
XorDef = { 0 0 = 0 ; 0 1 = 1; 1 0 = 1; 1 1 = 0; }
XorSpec = { 0 0 -- 0; 0 1 -- 1; 1 0 -- 1; 1 1 -- 0; }
```

Другие типы могут, например, более свободно трактовать возможные выходные значения, или же задавать дополнительные ограничения на входные значения и получать таким образом дополнительные свойства выходных значений. Фактически, тип — это свойство функции (утверждение о функции).

```
XorNeg = { 1 s.1 -- s.2, <Not s.1> : s.2 }
```

Можно попытаться получить XorNeg ⩽ XorSpec, в терминах пересечения спецификаций:

```
<HasType XorNeg XorSpec>
```

# Проверка на завершимость
Индуктивные типы.

```
ℕ {
  = ;
  1 e.1, <ℕ e.1> : = 1 e.1
}
```

Известные условия завершимости:
1. Длина аргумента: функция F завершима, если в рекурсивных вызовах используется только убывающий по длине аргумент.
2. Размер аргумента: функция F завершима, если на аргументах можно определить другую функцию G : dom F → ℕ, такую, что в рекурсивных вызовах используется аргумент меньшего размера.
3. Трансфинитная индукция.

# λ-исчисление с зависимыми типами
Для определения типов функций высшего порядка введём понятие функциональной переменной `f`, сопоставление которой успешно в точности для функций.
Определим виды, типы и термы λ-исчисления с зависимыми типами в виде трансляции
⟦ Type ⟧ = Type { f.FN, < Finite f.FN > -- f.FN }
В качестве контекстов используем простую последовательность переменных:
⟦ (x : A), (y : B), … ⟧ = t.x t.y …, < Type ⟦A⟧ > < Type ⟦B ⟧> … < HasType s.x ⟦A⟧ > < HasType s.y ⟦B⟧ > …
⟦ Var v ⟧ = t.v
⟦ Π(x : A).B ⟧ = { t.x, < HasType Type ⟦A⟧ > < HasType ⟦A⟧ t.x > -- t.b, < HasType Type ⟦B⟧ > < HasType ⟦B⟧ t.b > }
⟦ λ(x : A).N ⟧ = { t.x, < HasType Type ⟦A⟧ > < HasType ⟦A⟧ t.x > = ⟦ N ⟧ }
⟦ M N ⟧ = < ⟦M⟧ ⟦N⟧ >

# Нетривиальные правила редукции
s =~A~ t ⇔ I — отношение структуры типа идентичности между элементами типа A (элементы типа идентичности s = t имеют структуру типа I(s, t)).
<table style="font-size: 0.8em">
<tr>
<td>
J(B, u, v, a =~A~ b, ξ, x)   ⟶   **let**
$\qquad$    A~1~      ≡       A(u, **refl** u)
$\qquad$    A~2~      ≡       A(v, ξ)
$\qquad$    s =~A2~ t   ⇔       I~2~
$\qquad$    a~1~      ≡       a(u, **refl** u) : A~1~
$\qquad$    a~2~      ≡       a(v, ξ) : A~2~
$\qquad$    a'~1~    ≡       J(B, u, v, A, ξ, a~1~) : A~2~
$\qquad$    b~1~      ≡       b(u, **refl** u) : A~1~
</td>
<td>
$\qquad$    b~2~      ≡       b(v, ξ) : A~2~
$\qquad$    b'~1~   ≡       J(B, u, v, A, ξ, b~1~) : A~2~
$\qquad$    x~1~      ≡       **itoe**(**refl** a'~1~) : I~2~(a'~1~, a'~1~)
$\qquad$    x~2~      :       I~2~(a'~1~, b'~1~)
$\qquad$    x~2~    ≡ J(A~1~, a~1~, b~1~, (r, ρ) ↦ I~2~(a'~1~, J(B, u, v, A, ξ, r)), x, x~1~)
$\qquad$    z       ≡       λ (w : B) (ω : v =~B~ w) (a~wω~ : A(w, ω)). J(B, w, v, A, ξ ∘ ω^-1^, a~wω~)
$\qquad$    x~3~      ≡       J(B, u, v, (r, ρ) ↦ I~2~(z(r, ρ, a(r, ρ)), b'~1~), ξ, x~2~)
$\qquad$  **in**      J(B, u, v, I~2~(a~2~, z · b), ξ, x~3~) $\qquad$ .
</td>
</tr>
</table>

Как исследовать поведение таких сложных правил?

<span class="small">
 Правило редукции переноса вдоль идентичности ξ : u =~B~ v элемента другого типа идентичности x : a(t, σ) =~A~ b(t, σ). <div style="display: inline-block">В. А. Васенин,</div> <div style="display: inline-block">М. А. Кривчиков.</div> «Предметно-ориентированные языки с заданной формальной семантикой на основе лямбда-исчисления с зависимыми типами». Международная конференция «Мальцевские чтения-2014», Новосибирск, 2014.
</span>



# Проверка типов
Методы суперкомпиляции требуют адаптации для работы с функциями высших порядков.
Схема обоснования существования метода суперкомпиляции:

1. Для типов-значений с ограничениями (без перебора и с раскрытием переменных типа `t`)^1^
Определен. Существует также суперкомпилятор SCP4, который работает на языке Рефал-5.^2^

2. Новые функциональные переменные `f.1` в образцах имеют семантику, аналогичную образцу-паре скобок `(e.1)`, с единственным отличием — распознаются функциональные скобки. Функциональные переменные непрозрачны для сопоставления с образцом.

3. Суждения типизации для функциональных переменных пока не раскрываются, записываются в контекст синтаксически.

Тип ложных высказываний — «пустая» функция с единственной инструкцией `FAIL`. Тип истинных высказываний — общезначимая функция `{ e.1 = }`.

<span class="small">
^1^ А.П. Немытых. О суперкомпиляции (к 80-летию со дня рождения В.Ф. Турчина). Международная конференция
"Современные проблемы математики, информатики и биоинформатики", Новосибирск, 2011.
^2^ А.П. Немытых. Суперкомпилятор SCP-4. Общая структура. М.: URSS. 2007. 152 с.
</span>



# Связанные работы

Автоматическая верификация с использованием методов суперкомпиляции (ближе к теоретико-модельным методам):
- Климов А.В., Ключников И.Г., Романенко С.А. Автоматизированная верификация счетчиковых систем посредством предметно-ориентированной многорезультатной суперкомпиляции.
- A. P. Lisitsa and A. P. Nemytykh. Towards verification via supercompilation. In Proceedings of the 29th Annual International Computer Software and Applications Conference (COMPSAC’05), 25-28 July 2005, Edinburgh, Scotland, UK, pages 9–10. IEEE Computer Society, 2005.

Методы суперкомпиляции для автоматизированного доказательства эквивалентности термов в λ-исчислении высших порядков (без зависимых типов):
- I. G. Klyuchnikov and S. A. Romanenko. Proving the equivalence of higher-order terms by means of supercompilation. In Pnueli et al. [33], pages 193–205. 2009


# Литература

Схемы программ: А. П. Ершов. Введение в теоретическое программирование: беседы о методе. М.: Наука, 1977. 288 С.

Алгорифмы Маркова: А. А. Марков, Н. М. Нагорный. Теория алгорифмов. М.: Наука, 1984. 432 С.

Язык программирования Рефал: http://www.refal.net/rf5_frm.htm

Дополнительно: Turchin V.F. Cybernetic Foundations of Mathematics. 1983 (unpublished). 
