# Описание
Данный алгоритм предназначен для генерации графического отображения, а также скобочной последовательности филогенетических деревьев для заданной матрицы расстояний.

# Инструкция к запуску
Для работы с [программой](https://github.com/Raaazzy/linguistics/blob/main/program.ipynb) ее необходимо открыть в среде, поддерживающей python-блокноты (расширение .ipynb). Например: colab, vs code, pycharm и другие. <br>
Примеры входных данных продемонстрированы в кодовых ячейках раздела "Тестовые данные". <br>
Алгоритм принимает на вход:
- Нижнетреугольные матрицы
```py
matrix_first_example = np.array([
    [0, 0, 0, 0],
    [96, 0, 0, 0],
    [96, 92, 0, 0],
    [91, 87, 95, 0]])

labels_first_example = ['A', 'B', 'C', 'D']

result = start_multi_upgma(matrix_first_example, labels_first_example)

for res in result:
  print(res)
  tree = Phylo.read(StringIO(res), "newick")
  Phylo.draw(tree)
```
- Верхнетреугольные матрицы
```py
matrix_second_example = np.array([
    [0, 96, 96, 91],
    [0, 0, 92, 87],
    [0, 0, 0, 95],
    [0, 0, 0, 0]])

labels_second_example = ['A', 'B', 'C', 'D']

result = start_multi_upgma(matrix_second_example, labels_second_example, 0)

for res in result:
  print(res)
  tree = Phylo.read(StringIO(res), "newick")
  Phylo.draw(tree)

```
- Полные матрицы
```py
matrix_third_example = np.array([
    [0, 96, 96, 91],
    [96, 0, 92, 87],
    [96, 92, 0, 95],
    [91, 87, 95, 0]])

labels_third_example = ['A', 'B', 'C', 'D']

result = start_multi_upgma(matrix_third_example, labels_third_example)

for res in result:
  print(res)
  tree = Phylo.read(StringIO(res), "newick")
  Phylo.draw(tree)

```

Матрицы должны быть обязательно преобразованы в любой числовой формат и заполнены не null-значениями. 

Так же можно импортировать excel или csv таблицу (пример можно найти [тут](https://github.com/Raaazzy/linguistics/blob/main/example_1.csv) и преобразовать ее в матрицу для дальнейшей работы с программой с помощью данного кода:
```py
import pandas as pd

# Чтение CSV файла с использованием pandas
df = pd.read_csv('example_1.csv', sep=',')

# Получение одномерного массива названий столбцов (первая строка файла)
labels_fourth_example_raw = df.columns[1:].to_numpy()
labels_fourth_example = np.array(labels_fourth_example_raw)

# Получение двумерного массива чисел
data = df.iloc[:, 1:].to_numpy(dtype=float)
matrix_fourth_example = np.array(data, dtype=float)

result = start_multi_upgma(matrix_fourth_example, labels_fourth_example)

for res in result:
  print(res)
  tree = Phylo.read(StringIO(res), "newick")
  Phylo.draw(tree)
```
