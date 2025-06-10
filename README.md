# Прогнозирование оттока клиентов «Бета-Банка»

Модель машинного обучения для предсказания вероятности ухода клиентов из «Бета-Банка».  
Проект направлен на удержание текущих клиентов, что экономически выгоднее, чем привлечение новых.

## 🎯 Цель проекта

- Спрогнозировать, уйдёт ли клиент из банка в ближайшее время (бинарная классификация)
- Достичь значения *F1*-меры не менее 0.59
- Измерить и сравнить метрику *AUC-ROC* с *F1*-мерой
- Выявить ключевые факторы, влияющие на отток клиентов

## 💡 Использованные технологии

- Python 3.x
- pandas, numpy, matplotlib, seaborn, sklearn
- DecisionTreeClassifier, RandomForestClassifier, LogisticRegression
- StandardScaler, OrdinalEncoder, train_test_split
- Метрики: f1_score, roc_auc_score, accuracy_score, precision_score, recall_score
- Jupyter Notebook

## 🧪 Как запустить проект

```bash
git clone https://github.com/kagor4/Churn-Prediction-for-Beta-Bank.git
cd Churn-Prediction-for-Beta-Bank
pip install -r requirements.txt
```

Затем откройте и запустите файл `projectgithub_update2.py` или ноутбук с аналогичным кодом в Jupyter. Убедитесь, что датасет `Churn.csv` доступен в папке `/datasets/`.

## 📊 Описание данных

Датасет содержит исторические данные о поведении клиентов и расторжении договоров:
- **Churn.csv**:
  - `RowNumber` — индекс строки (удалён)
  - `CustomerId` — идентификатор клиента
  - `Surname` — фамилия (удалена)
  - `CreditScore` — кредитный рейтинг
  - `Geography` — страна проживания (France, Germany, Spain)
  - `Gender` — пол (Male, Female)
  - `Age` — возраст
  - `Tenure` — стаж клиента (лет)
  - `Balance` — баланс на счёте
  - `NumOfProducts` — количество продуктов банка
  - `HasCrCard` — наличие кредитной карты (0/1)
  - `IsActiveMember` — активность клиента (0/1)
  - `EstimatedSalary` — предполагаемая зарплата
  - `Exited` — целевой признак (0 — остался, 1 — ушёл)
- **Предобработка**:
  - Пропуски в `Tenure` заполнены равномерно
  - Категориальные признаки (`Geography`, `Gender`) закодированы методом one-hot encoding
  - Числовые признаки стандартизированы с помощью StandardScaler
  - Удалены неинформативные столбцы (`RowNumber`, `Surname`)

## 🔍 Краткие результаты

- **Лучшая модель**: RandomForestClassifier (с увеличением выборки)
- **Метрики на тестовой выборке**:
  - *F1*-мера: 0.61 (цель ≥ 0.59 достигнута)
  - *ROC AUC*: 0.85
  - Accuracy: 0.82
  - Precision: 0.57
  - Recall: 0.66
- **Ключевые факторы** (по важности признаков):
  - `Age`, `Balance`, `NumOfProducts`, `IsActiveMember` — наиболее значимые
  - Меньшее влияние: `CreditScore`, `EstimatedSalary`
- **Методы борьбы с дисбалансом**:
  - Взвешивание классов (`class_weight='balanced'`)
  - Увеличение выборки (upsampling, repeat=4)
  - Уменьшение выборки (downsampling, fraction=0.3)
- **Основные выводы**:
  - RandomForestClassifier с upsampling показал лучший баланс между Precision и Recall
  - Дисбаланс классов (80% — остались, 20% — ушли) существенно влияет на качество модели
  - Увеличение выборки и взвешивание классов дают схожие результаты, но upsampling предпочтительнее из-за более высокого Recall
  - LogisticRegression показала худшие результаты (F1 ≈ 0.28–0.49)
- **Рекомендации**:
  - Использовать RandomForestClassifier с upsampling для прогнозирования
  - Сфокусироваться на удержании активных клиентов с высоким балансом и возрастом
  - Исследовать дополнительные признаки (например, частота транзакций)
  - Провести A/B-тестирование для оценки влияния удерживающих мер

## 📁 Структура проекта

```
📦 Churn-Prediction-for-Beta-Bank/
├── projectgithub_update2.ipynb  # анализ и обучение модели
├── requirements.txt             # зависимости
└── README.md                    # описание проекта
```

## ✅ TODO

- Исследовать другие алгоритмы (например, XGBoost, CatBoost)
- Провести анализ SHAP для интерпретации важности признаков
- Добавить визуализацию ROC-кривых для всех моделей
- Интегрировать временные данные о транзакциях клиентов

## © Автор

Автор: [kagor4](https://github.com/kagor4)  
