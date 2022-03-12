---
# Front matter
lang: ru-RU
title: "Лабораторная работа №5"
subtitle: "Модель хищник-жертва"
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

* Построить модель «хищник - жертва» Лотки - Вольтерры:
  * Построить следующие графики зависимости:
    *  x от y.
    * x(t), y(t).
  * Найти стационарное состояние системы

# Задание №49

Для модели «хищник-жертва»:
$$
\begin{cases} \frac{\partial x}{\partial t} = -0.76x(t)+0.082x(t)y(t) \\ \frac{\partial y}{\partial t} = 0.62y(t)-0.039x(t)y(t) \end{cases}
$$
Постройте график зависимости численности хищников от численности жертв, а также графики изменения численности хищников и численности жертв при следующих начальных условиях: 
$$
x_0 = 8 \\
y_0 = 20
$$
Найдите стационарное состояние системы.

# Краткая теоретическая справка

Простейшая модель взаимодействия двух видов типа «хищник-жертва» — модель Лотки-Вольтерры. Данная двувидовая модель основывается на следующих предположениях:

1. Численность популяции жертв x и хищников y зависят только от времени (модель не учитывает пространственное распределение популяции на занимаемой территории)
2. В отсутствии взаимодействия численность видов изменяется по модели Мальтуса (по экспоненциальному закону), при этом число жертв увеличивается, а число хищников падает
3. Естественная смертность жертвы и естественная рождаемость хищника считаются несущественными
4. Эффект насыщения численности обеих популяций не учитывается
5. Скорость роста численности жертв уменьшается пропорционально численности хищников

$$
\begin{cases} \frac{\partial x}{\partial t} = ax(t)+bx(t)y(t) \\ \frac{\partial y}{\partial t} = -cy(t)-dx(t)y(t) \end{cases}
$$

В этой модели x – число жертв, y - число хищников. Коэффициент a описывает скорость естественного прироста числа жертв в отсутствие хищников, c - естественное вымирание хищников, лишенных пищи в виде жертв. Вероятность взаимодействия жертвы и хищника считается пропорциональной как количеству жертв, так и числу самих хищников xy. Каждый акт взаимодействия уменьшает популяцию жертв, но способствует увеличению популяции хищников (члены -bxy и dxy в правой части уравнения).

Математический анализ этой (жесткой) модели показывает, что имеется стационарное состояние (положение равновесия, не зависящее от времени решения). Если начальное состояние будет другим, то это приведет к периодическому колебанию численности как жертв, так и хищников, так что по прошествии некоторого времени система возвращается в начальное состояние. Стационарное состояние системы будет в точке: 
$$
x_0 = \frac{c}{d}, y_0 = \frac{a}{b}
$$
Если начальные значения задать в стационарном состоянии 
$$
x(0)=x_0, y(0)=y_0
$$
, то в любой момент времени численность популяций изменяться не будет. При малом отклонении от положения равновесия численности как хищника, так и жертвы с течением времени не возвращаются к равновесным значениям, а совершают периодические колебания вокруг стационарной точки. Амплитуда колебаний и их период определяется начальными значениями численностей x(0), y(0). Колебания совершаются в противофазе.

# Выполнение лабораторной работы

**Код работы**

model lab05

constant Real a=0.76; //смертность хищников
constant Real b=0.082; //прирост жертв
constant Real c=0.62; //прирост хищников
constant Real d=0.039; //смертность жертв
Real x;
Real y;

initial equation //начальные условия
x=8;
y=20;

equation
der(x)=-ax+bxy;
der(y)=cy-dxy;

end lab05;



**Стационарное состояние системы**
$$
x_0=\frac{0.62}{0.039}
\\
y_0=\frac{0.76}{0.082}
$$
**Графики**

*Зависимость изменения численности хищников от изменения численности жертв (рис.01).*

<figure>
    <img src = screen\5_1.JPG alt = "жертвы">
    <figcaption>рис.01</figcaption>
</figure>




*Зависимость численности хищиников и жертв от времени (рис.02).*

<figure>
    <img src = screen\5_2.JPG alt = "время">
    <figcaption>рис.02</figcaption>
</figure>



# Вывод

Построили модель «хищник - жертва» Лотки - Вольтерры.

Построили следующие графики зависимостей: x от y и  x(t), y(t).

Нашли стационарное состояние системы.

# Список литературы

Кулябов Д.С "Лабораторная работа №5": https://esystem.rudn.ru/pluginfile.php/1343813/mod_resource/content/2/Лабораторная%20работа%20№%204.pdf
