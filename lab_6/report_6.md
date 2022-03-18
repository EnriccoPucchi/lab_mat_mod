---
# Front matter
lang: ru-RU
title: "Лабораторная работа №6"
subtitle: "Задача об эпидемии"
author: "Уваров Андрей Дмитриевич"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

1. Нужно построить графики изменения числа особей в каждой из трех групп при помощи простейшей модели эпидемии.
2. Рассмотреть течение эпидемии в двух случаях.

# Задание №49

На одном острове вспыхнула эпидемия. Известно, что из всех проживающих на острове  (N=5 505) в момент начала эпидемии (t=0) число заболевших людей (являющихся распространителями инфекции) I(0)=45, А число здоровых людей с иммунитетом к болезни R(0)=3. Таким образом, число людей восприимчивых к болезни, но пока здоровых, в начальный момент времени S(0)=N-I(0)- R(0). Постройте графики изменения числа особей в каждой из трех групп. Рассмотрите, как будет протекать эпидемия в случае: 

1) Если I(0) > I*; 
2) Если I(0) <= I*;

# Краткая теоретическая справка

Предположим, что некая популяция, состоящая из N особей, (считаем, что популяция изолирована) подразделяется на три группы.

- S(t) — восприимчивые к болезни, но пока здоровые особи
- I(t) — это число инфицированных особей, которые также при этом являются распространителями инфекции
- R(t) — это здоровые особи с иммунитетом к болезни.

До того, как число заболевших не превышает критического значения I считаем, что все больные изолированы и не заражают здоровых. Когда I(t)>I*, тогда инфицирование способны заражать восприимчивых к болезни особей.

Таким образом, скорость изменения числа S(t) меняется по следующему закону:
$$
 \frac{\partial S}{\partial t} = \begin{cases} - \alpha S, если \ I(t)>I^* \\ 0, если \ I(t) \leq I^* \end{cases}
$$
Поскольку каждая восприимчивая к болезни особь, которая, в конце концов, заболевает, сама становится инфекционной, то скорость изменения числа инфекционных особей представляет разность за единицу времени между заразившимися и теми, кто уже болеет и лечится, т.е.:
$$
 \frac{\partial I}{\partial t} = \begin{cases} \alpha S - \beta I, если \ I(t)>I^* \\  - \beta I, если \ I(t) \leq I^* \end{cases}
$$
А скорость изменения выздоравливающих особей (при этом приобретающие иммунитет к болезни)
$$
\frac{\partial R}{\partial t} = \beta I
$$
Постоянные пропорциональности:

- $$
  \alpha
  $$

   — коэффициент заболеваемости

- $$
  \beta
  $$

  — коэффициент выздоровления

Для того, чтобы решения соответствующих уравнений определялось однозначно, необходимо задать начальные условия. Считаем, что на начало эпидемии в момент времени t = 0 нет особей с иммунитетом к болезни R(0)=0, а число инфицированных и восприимчивых к болезни особей I(0) и S(0) соответственно. Для анализа картины протекания эпидемии необходимо рассмотреть два случая: I(0) > I* и I(0) <= I*

# Выполнение лабораторной работы

**Код работы**

model lab06
constant Real a = 0.01; //коэф заболеваемости
constant Real b = 0.02; //коэф выздоровления
constant Real N = 5424; //общее число популяции


Real R; // здоровые, с иммунитетом
Real I; // заболевшие
Real S; // здоровые, в зоне риска

initial equation
R = 9;
I = 145; //кол-во заболевших в t = 0
S = N-I-R;

equation
//Случай 1: I>I*

der(S) = - a * S;
der(I) = a * S-b * I;
der(R) = b * I; 


//Случай 2: I<=I*

/*
der(S) = 0;
der(I) = -b * I;
der(R) = b * I; 
*/

end lab06;



**Графики**

*Случай 1: I > I*  (рис.01)*

<figure>
    <img src = screen\6_1.jpg alt = "I > I*">
    <figcaption>рис.01</figcaption>
</figure>



*Случай 2: I <= I*  (рис.02)*

<figure>
    <img src = screen\6_2.jpg alt = "I <= I*">
    <figcaption>рис.02</figcaption>
</figure>




# Вывод

1. Построил графики изменения числа особей в каждой из трех групп при помощи простейшей модели эпидемии.
2. Рассмотрел течение эпидемии в двух случаях.

# Список литературы

Кулябов Д.С "Лабораторная работа №6": https://esystem.rudn.ru/pluginfile.php/1343817/mod_resource/content/2/Лабораторная%20работа%20№%205.pdf
