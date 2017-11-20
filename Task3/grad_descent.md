﻿Материалы

http://www.machinelearning.ru/wiki/index.php?title=%D0%9C%D0%B5%D1%82%D0%BE%D0%B4_%D0%B3%D1%80%D0%B0%D0%B4%D0%B8%D0%B5%D0%BD%D1%82%D0%BD%D0%BE%D0%B3%D0%BE_%D1%81%D0%BF%D1%83%D1%81%D0%BA%D0%B0
Matplotlib User Guide: http://matplotlib.org/users/index.html

В данной работе рассмотрим линейную регрессию - один из наиболее хорошо изученных методов машинного обучения, позволяющий прогнозировать значения количественного признака в виде линейной комбинации прочих признаков с параметрами - весами модели, и градиентными методами для оптимизации параметров модели (с точки зрения минимальности некоторого функционала ошибки - MSE).

Предварительные шаги.
В работе будем предсказывать рост человека, по его весу.
Загрузите данные weights_heights.csv, просмотрите первые 5 объектов, и постройте по всей выборке scatter plot. (можно воспользоваться методом plot у DataFrame'а).
Что можно сказать по данным? Можно ли использовать линейную модель?

## Задача 1. Нахождение параметров модели аналитически

y = X*w, y - рост, X - матрица признаков, w - веса модели.

Поскольку приближаем линейно моделью a(x) = w0 + w1*x, то в матрицу признаков необходимо добавить константный признак при w0. Составьте соответсвующую матрицу X, где первая колонка = 1, а вторая значениям веса.
Найдите значения w_i, решая систему X^T * X * w = X^T*y, где X^T - транспонированная матрица X. (используйте метод np.linalg.solve)
Полученные значения - первый ответ. Выведите значение признаков через пробел с точностью до 3 знака после запятой.

## Задача 2. Нахождение параметров модели минимизацией функционала ошибки градиентным спуском.

Функционал ошибки (MSE) имеет вид: Q(a(x), y) = 1/n*Sum(yi - a(x))^2 -> 1/n*Sum(yi - (wo + w1*xi))^2.

Можно ли воспользоваться градиентным методом? Почему?
Как выглядит итерационаня формула для приближения wi? Запрограммируйте эту функцию.
Создайте функцию - grad_desent(X, y, w_init, eta=1e-4, max_iter=1e4, min_weight_dist=1e-8), для вычисления w. w_init - начальное значение для w, eta - шаг градиентного спуска, min_weight_dist - точность метода = растоянию между w_n+1 и w_n, max_iter - максимальное количество итераций.
Полученные значения с точностью до 3 знака после запятой - второй ответ.

## Задача 3. Нахождение параметров модели минимизацией функционала ошибки стохатическим градиентным спуском.

Ситуация аналогична Заданию 2, только теперь вычисление ошибки осуществляется не на всем множестве объектов на каждой итерации, а на одном случайном объекте.
Для получения случайного индекса воспользуйтесь np.random.randint(X.shape[0]).
Третий ответ - полученные значения весов с точностью до 3х знаков. При вычислении зафисируйте np.random.seed(42) - для воспроизведения псевдослучайно последовательности.


Критерии оценки:
1. Для каждого из градиентного метода постройте график изменения средней квадратичной ошибки:
err = 1/n*sum(y - yi)^2 - y-актуальное значение роста, yi - i-е итерационное значение веса, n - размер выборки.

2. Для каждой пары весов постройте прямую на "множестве данных" - первый график