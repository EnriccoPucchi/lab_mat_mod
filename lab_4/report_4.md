---
# Front matter
lang: ru-RU
title: "Лабораторная работа №4"
subtitle: "Модель гармонических колебаний"
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

- Построить фазовый портрет гармонического осциллятора;
- Решить уравнения гармонического осциллятора.

# Задание №49

Постройте фазовый портрет гармонического осциллятора и решение уравнения гармонического осциллятора для следующих случаев:

   1. Колебания гармонического осциллятора без затуханий и без действий внешней силы  
      $$
      \ddot {x} + 18x = 0
      $$
      
2. Колебания гармонического осциллятора c затуханием и без действий внешней силы

$$
\ddot {x} +8\dot {x}+ 2x = 0
$$

3. Колебания гармонического осциллятора c затуханием и под действием внешней силы
   $$
   \ddot {x} +3\dot {x}+ 7x = 3sin(7t)
   $$

На интервале 
$$
t \in [0; 73]
$$
 (шаг 0.05) с начальными условиями 
$$
x_0 = 1.3, y_0 = -0.3
$$

# Краткая теоретическая справка

Движение грузика на пружинке, маятника, заряда в электрическом контуре, а также эволюция во времени многих систем в физике, химии, биологии и других науках при определенных предположениях можно описать одним и тем же дифференциальным уравнением, которое в теории колебаний выступает в качестве основной модели. Эта модель называется линейным гармоническим осциллятором. Уравнение свободных колебаний гармонического осциллятора имеет следующий вид:
$$
\ddot {x} +2\gamma\dot{x}+ w_0^2x = 0
$$
где x – переменная, описывающая состояние системы (смещение грузика, заряд конденсатора и т.д.), gamma - параметр, характеризующий потери энергии (трение в механической системе, сопротивление в контуре), w_0 - собственная частота колебаний, t- время.

 При отсутствии потерь в системе получаем  уравнение(*) консервативного осциллятора энергия колебания которого сохраняется во времени.
$$
\ddot {x} + w_0^2x = 0 													
$$
Для однозначной разрешимости уравнения второго порядка (*) необходимо задать два начальных условия(**) вида

​									
$$
\begin{equation*} 
  \begin{cases} 
    x(t_0) = x_0
    \\
    \dot x(t_0) = y_0 
  \end{cases}
\end{equation*}
$$
Уравнение второго порядка (*) можно представить в виде системы двух уравнений(**\*) первого порядка:
$$
\begin{equation*} 
  \begin{cases} 
    \dot x = y
    \\
    \dot y = -w^2_0x 
  \end{cases}
\end{equation*}
$$
Начальные условия (\*\*) для системы (\*\*\*) примут вид:
$$
\begin{equation*} 
  \begin{cases} 
    x(t_0) = x_0
    \\
    y(t_0) = y_0 
  \end{cases}
\end{equation*}
$$
Независимые переменные x, y определяют пространство, в котором «движется» решение. Это фазовое пространство системы, поскольку оно двумерно будем называть его фазовой плоскостью. Значение фазовых координат x, y в любой момент времени полностью определяет состояние системы. Решению уравнения движения как функции времени отвечает гладкая кривая в фазовой плоскости. Она называется фазовой траекторией. Если множество различных решений (соответствующих различным  начальным условиям) изобразить на одной фазовой плоскости, возникает общая картина поведения системы. Такую картину, образованную набором фазовых траекторий, называют фазовым портретом.

# Выполнение лабораторной работы

**Случай 1: **

```
model lab_4_1

constant Real w=sqrt(18);

Real x;
Real y;

initial equation
x=-0.3;
y=1.3;

equation
der(x)=y;
der(y)=-w*w*x;

end lab_4_1;
```



График первого случая (рис.01).

<figure>
    <img src = screen\4_1.JPG alt = "График первого случая">
    <figcaption>рис.01</figcaption>
</figure>





**Случай 2: **

```
model lab_4_2

constant Real w=sqrt(18);
constant Real g=(8/2);

Real x;
Real y;

initial equation
x=1.3;
y=-0.3;

equation
der(x)=y;
der(y)=-2*g*der(x)-w*w*x;

end lab_4_2;

```



График второго случая (рис.02).

<figure>
    <img src = screen\4_2.JPG alt = "График второго случая">
    <figcaption>рис.02</figcaption>
</figure>




**Случай 3: **

```
model lab_4_3

constant Real w=sqrt(18);
constant Real g=(8/2);

Real x;
Real y;

initial equation
x=1.3;
y=-0.3;

equation
der(x)=y;
der(y)=-2*g*der(x)-w*w*x - 3*sinus(7*t);


end lab_4_3;

```



График третьего случая (рис.03).

<figure>
    <img src = screen\4_3.JPG alt = "График третьего случая">
    <figcaption>рис.03</figcaption>
</figure>


# Вопросы к лабораторной работе

1. **Запишите простейшую модель гармонических колебаний** 

   Простейшим видом колебательного процесса являются простые гармонические колебания, которые описываются уравнением.
   $$
   x = x_m cos (ωt + φ0).
   $$

2. **Дайте определение осциллятора.**

   Осциллятор — система, совершающая колебания, то есть показатели которой периодически повторяются во времени.

3. **Запишите модель математического маятника.** 

   Линейное дифференциальное уравнение 
   $$
   \frac{d^2 \alpha}{d t^2} + \frac{g}{L} \alpha = 0
   $$
   ​																			или
   $$
   \frac{d^2 \alpha}{d t^2} + \omega^2 \alpha = 0
   $$

4.  **Запишите алгоритм перехода от дифференциального уравнения второго порядка к двум дифференциальным уравнениям первого порядка.** 

   Пусть у нас есть дифференциальное уравнение 2-го порядка: 
   $$
    \ddot {x} + w_0^2x = f(t)
   $$
   Для перехода к системе уравнений первого порядка сделаем замену (это метод Ранге-Кутты): 
   $$
   y = \dot{x}
   $$
   Тогда получим систему уравнений: 
   $$
   \begin{cases} y = \dot{x} \\
   \dot{y} = - w_0^2x \end{cases}
   $$

5.  **Что такое фазовый портрет и фазовая траектория?**

   Фазовый портрет исследуемой системы — это совокупность фазовых траекторий для всевозможных начальных условий. Его можно рассматривать как интегральное многообразие.

   Фазовая траектория — кривая в фазовом пространстве, составленная из точек, представляющих состояние динамической системы в последовательные моменты времени в течение всего времени эволюции.


# Вывод

Освоил фазовый портрет гармонического осциллятора и решил уравнения гармонического осциллятора:

1. Колебания гармонического осциллятора без затуханий и без действий внешней силы.
2. Колебания гармонического осциллятора c затуханием и без действий внешней силы.
3. Колебания гармонического осциллятора c затуханием и под действием внешней силы.



# Список литературы

Кулябов Д.С "Лабораторная работа №4": https://esystem.rudn.ru/pluginfile.php/1343809/mod_resource/content/2/Лабораторная%20работа%20№%203.pdf

<figure>