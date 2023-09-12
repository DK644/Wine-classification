# Wine-classification
Проект по классификации вина с использованием модели случайного леса, использовалось несколько методов отбора значимых признаков, в том числе метод главных компонент, был сделан вывод, что низкое качество классификации вызвано несбалансированностью классов
Подробнее рассмотрим что было сделано:
1. Был визуализирован датасет и выведены основные его статистики, был сделан вывод что большая часть столбцов распредлелена симметрично из за близости среднего и медианного значений.
2. С помощью критерий шапиро-Уилка был сделан вывод, что распределение столбцов не соответствует нормальному. 
Были построены гистограммы, показывающие распределение каждого столбца, с их помощью были определены и удалены выбросы
После удаления выбросов снова производилась проверкана соответствие нормальному распределению, но данные так и остались распределены ненормально. 
3. Далее была составлена матрица корреляции, которая показала попарную взаимосвязь между столбцами
4. В качестве модели прогноза использовался Случайный лес с 35-ю деревьями
5. Обучение модели было вложено в пайплайн, внутри которого данные предобрабатывались (стандартизировались), обучалась модель, тестировалась на тестовых данных и выводилась метрика.
6. Было предложено 4 варианта отбора признаков:
   - Использование всех доступных признаков для обучения
   - Удаление зависимых столбцов согласно здравому смыслу, удалялись столбцы, которые имели явную связь с другими, также с помощью частного коэффициента корреляции связь столбцов с целевой переменной была проверена на ложную корреляцию, что помогло выявить два ложных столбца.
   - Выбор наиболее значимых столбцов используя "исчерпывающий отбор признаков" с помощью класса ExhaustiveFeatureSelector
   - Используя метод главных компонент (PCA)
  
   В результате выбранная метрика f1 с макроусреднением не поднималась выше 0.348, наилучший результат был показан при использовании всех признаков.

Была выдвинута гипотеза, что в низкой метрике виновата плохпя сбалансированность классов, тогда исходный набор данных был разхделён на два: с низким количеством представителей своего класса и с высоким, далее применялся обычный пайплайн случайного леса и стандартизацией, в итоге для группы классов с большим числом представителей метрика f1 составила 0.694, а для классом с низким числом представителей 0.588, что подтвердило гипотезу о том, что плохая сбалансированность отрицательно сказывается на качестве обучения модели. 
