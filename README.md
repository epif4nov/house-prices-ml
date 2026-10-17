# California Housing: regression study

Учебный ML-проект: исследование данных, конструирование признаков и сравнение моделей для оценки медианной стоимости жилья в районах Калифорнии.

**Python 3.12+ · pandas · NumPy · matplotlib · scikit-learn · Jupyter**

## Что реализовано

- EDA: распределения, география, корреляции и отношения признаков.
- Stratified holdout по категории дохода; фиксированные seeds.
- Pipeline: заполнение пропусков, дополнительные признаки, масштабирование, one-hot encoding.
- LinearRegression, DecisionTreeRegressor и RandomForestRegressor.
- Cross-validation и GridSearchCV: preprocessing обучается внутри каждого fold.
- Финальная RMSE на отложенной выборке после выбора модели.

## Воспроизведение

```sh
python -m venv .venv
source .venv/bin/activate
# Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m jupyterlab Housing.ipynb
```

Запускайте notebook из корня репозитория последовательно сверху вниз. Архив данных уже включён: повторный сетевой download не нужен. Загрузка проверяет SHA-256 и читает только ожидаемый housing.csv, без произвольного extractall.

Grid search содержит 90 обучений на пяти fold и использует два процесса; время зависит от машины. Обучение не является мгновенным smoke-тестом.

## Проверенный результат

Основной notebook выполнен последовательно: 70 code cells, без ошибок. В проверенном запуске held-out RMSE составила **47 873.26**; это результат конкретного окружения, а не обещание качества на новых данных. Оценки CV дополнительно проверяются на конечность: ошибочный fold не должен превращаться в незаметный NaN.

## Структура

```text
Housing.ipynb                         Основное исследование недвижимости
datasets/housing/housing.tgz           Исходный архив California Housing
notebooks/mnist-exploration.ipynb      Сохранённый незавершённый эксперимент
requirements.txt                      Только зависимости этого исследования
```

## Интерпретация

RMSE измеряется в единицах стоимости исходного датасета и не является точностью в процентах. Training error не заменяет оценку на holdout. Точные значения зависят от версий библиотек; диапазоны requirements не являются lockfile.

MNIST вынесен из основного notebook: это другая задача, требующая скачивания с OpenML; завершающий эксперимент не закончен и не входит в подтверждённый запуск.

## Источник и ограничения

Исследование основано на California Housing и примерах из [Hands-On Machine Learning — Aurélien Géron](https://github.com/ageron/handson-ml). Это учебное воспроизведение и доработка, а не собственный датасет или новая ML-методика. Нет CatBoost/LightGBM, сервиса предсказаний или мониторинга качества. Следующие шаги — анализ ошибок по сегментам и сохранение полного fitted pipeline.
