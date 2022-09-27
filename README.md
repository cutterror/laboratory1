# Анализ данных и искуственный интеллект Лабараторная № 1 конструкция языка python на примере реализации линейной регрессии
Отчет по лабораторной работе #1 выполнил:
- Демина Анастасия Викторовна
- РИ210942
- Отметки о выполнении задания (undone-#, done-*)

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

Структура отчета

## Цели работы
Ознакомиться с основными операторами языка Python на примере реализации линейной регрессии.

## Задание 1
 Написать программы Hello world на Python и Unity

## Задание 2
 В разделе "ход работы" пошагово выполнить каждый пунк с описание и примром реализации задачи по теме лабораторной работы

## Задание 3
 Изучить код на Python и ответить на вопросы:
   1)Должна ли величина "loss" стремиться к 0 при изменении исходных данных? Ответить на вопрос, привести пример кода, подтверждающий ответ
   2)Какова роль параметра "Lr" ? Ответить на вопрос, привести пример кода, подтверждающий ответ (можно изменять значение параметра).


# Ход работы:


## Задание 1

1) Создала файл блокнота в Google-colab. Написала команду вывода "Hello world!" в консоль. Сохранила файл на Google Диске 
2) Создала новый 3D проект в Unity. Создала скрипт и написала скрипт на C#, выводящую "Hello World"
(скриншоты в папке 'задание1')


## Задание 2

1) Произвела подготовку данных для работы с алгоритмом линейной регрессии. Установила 10 видов данных случайным образом в линейной зависимости;
2) Определила связанные функции: функцию модели, функцию потерь, функцию оптимизации.
3) Выполнила шаги 1-6 (скриншоты в папке 'задание2'). Из скриншотов заметна прямая зависимость между увеличением значения параметра и точностью графика. При низких значениях параметра график случайным образом отклоняется от точек.
```py
import numpy as np
import matplotlib.pyplot as  plt
%matplotlib inline

x = [1, 2, 13, 16, 25, 36, 49, 56, 76, 84]
x = np.array(x)
y = [13, 53, 454, 560, 600, 710, 870, 900, 1100, 1360]
y = np.array(y)

# 3 Step 1.1
#Initialize parameters and display
a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
Lr = 0.000001

# The basic linear regression model is wx+b, and since this is a two-dimensional space, the model is ax+b
# модель линейной регрессии
def model(a, b, x):
  return a * x + b

# Take most commonly used loss function of linear regression model is the loss function of mean variance difference
# возьмем самую простую в использовании модель функцию линейной регрессии
def loss_function(a, b, x, y):
  num = len(x)
  prediction = model(a, b, x)
  return (0.5 / num) * (np.square(prediction - y)).sum()

# The optimization function mainly USES partial derivatives to update twj parameters a and b
def optimize(a, b, x, y):
  num = len(x)
  prediction = model(a, b, x)
  # Update the values of A and B by finding the partial derivatives of the loss function on a and b
  da = (1.0 / num) * ((prediction - y) * x).sum()
  db = (1.0 / num) * (prediction - y).sum()
  a = a - Lr * da
  b = b - Lr * db
  return a, b

# iterated function, return a and b
def iterate (a, b, x, y, times):
  for i in range(times):
    a, b = optimize(a, b, x, y)
  return a, b


# 3 Step 1.2
#For the first iteration, the parameter values, losses, and visualization after the iteration are displayed
a, b = iterate(a, b, x, y, 10000)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss, Lr)
plt.scatter(x,y)
plt.plot(x,prediction)


plt.scatter(x, y)
```

## Задание 3

- Для исследования роли параметра Lr, добавила вывод его значения на консоль.
- В ходе исследования делала скриншоты (папка 'задание3')

## 1) 

Изначальные значения: (скриншот 1)
```py
x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
x = np.array(x)
y = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
y = np.array(y)
```
Увеличила значения в массиве x: (скриншот 2) 
```py
x = [1000, 2000, 3000, 4000, 5000, 6000, 7000, 8000, 9000, 10000]
x = np.array(x)
y = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
y = np.array(y)
```
-значение loss многократно увеличилось

## Вывод:
  Значение величины loss имеет прямую зависимость от величины значений в массивах x и y. При малых значениях в массивах x и y loss стремится к нулю.

## 2) 

Изначальные значения: (скриншот 3)
```py
Lr = 0.000001
```
Уменьшила значение: (скриншот 4)
```py
Lr = 0.0000000000000001
```
Увеличила значение (скриншот 5)
```py
Lr = 0.01
```
## Вывод:
   Параметр Lr имеет обратную зависимость с параметром loss

## Итоги работы:
В ходе работы ознакомилась с основами языка Python и его операторами, изучила линейную регрессию, рассмотрела зависимости её параметров.

## Приложение
### Основная литература:
1) Грас Дж. Data science. Наука о данных с нуля: Пер. с англ. - СПб.: БХВ- Петербург, 2020.-336с.: ил.
2) Николаенко С.И., Кадурин А.А., Архангельская Е.О. Глубокое обучение.-СПб.:Питер,2017.-480с.
3) Гудфеллоу Я., Бенджио И., Курвилль А. Глубокое обучение / пер. с анг.
А.А.Слинкина.-2-е изд., испр. - Москва : ДМК Пресс, 2018. - 652с.: цв. ил.
4) Шолле Ф. Глубокое обучение на Python/ - СПб.: Питер, 2018. - 400с.

### Дополнительная литературра:
1) Клетте, Рейнхард. Компьютерное зрение. Теория и алгоритмы. -М.: ДМК Пресс, 2019
2) Пойнтер, Ян. Программируем с PyTorch. Создание приложений глубокогго обучения. -СПб: из-во Питер, 2020. -256 с.
3) Траск Эндрю. Грокаем глубокое обучение. -СПб.: Питер, 2019. - 352 с.
4) Ян, Э.С. Программирование компьютерного зрения на языке Python / Э.С. Ян; перевод с английского А.А. Слинкин. -Москва: ДМК Пресс, 2016. - 312 с.
5) Он-лайн курс "Нейронные сети и компьютерное зрение". - URL: https://stepik.org/course/50352/promo.
6) приведенный в работе код: https://colab.research.google.com/drive/1UUPyIFC8FeTLLJSpfxn875iYEN-n9Y_8
