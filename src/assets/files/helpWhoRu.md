<span style="color: #000;">Этот скрипт нужно писать на языке Python. Если тебе незнакомы основы языка или тебе нужно освежить память, используй <a href="https://docs.python.org/3/tutorial/index.html" target="_blank" rel="nofollow">эту ссылку</a>.</span>

<span style="color: #000;">В зависимости от задачи, уровень может генерироваться по-разному. При нажатии на кнопку "Перегенерировать уровень" получаются разные варианты первоначальных условий. Иногда уровень будет постоянным с одними и теми же начальными условиями.</span>

<span style="color: #000;">Для прохождения уровня необходимо импортировать модуль player, который используется для управления персонажем на игровом поле:</span>
```python
import player
```

<span style="color: #000;">Управление персонажем осуществляется следующими методами:</span>
* ```python
    player.go_left(n)
    ```
    <p style="color: #000;">Движение на n клеток влево. Значение по умолчанию: 1.</p>

* ```python
    player.go_right(n)
    ```
    <p style="color: #000;">Движение на n клеток вправо. Значение по умолчанию: 1.</p>

* ```python
    player.go_up(n)
    ```
    <p style="color: #000;">Движение на n клеток вверх. Значение по умолчанию: 1.</p>

* ```python
    player.go_down(n)
    ```
    <p style="color: #000;">Движение на n клеток вниз. Значение по умолчанию: 1.</p>

* ```python
    player.wait(n)
    ```
    <p style="color: #000;">Ждать n ходов. Значение по умолчанию: 1. Максимально допустимое значение: 100.</p>
    
* ```python
    player.look
    ```
    <p style="color: #000;">Существует два варианта вызова метода:</p>

    ```python
    player.look(X, Y)
    ```
    <p style="color: #000;">Возвращает единственное число в зависимости от того, что находится в указанном направлении.</p>

    ```python
    player.look([X1, Y1], [X2, Y2], [X3, Y3], ...) 
    ```
    <p style="color: #000;">Возвращает массив чисел в зависимости от того, что находится в указанном направлении, который будет содержать столько чисел, сколько клеток проверяется.</p>
    <p style="color: #000;">
    Возвращаемые значения:<br>
    0 - непроходимая местность<br>
    1 - дорога<br>
    2 - вирус<br>
    3 - человек<br>
    4 - маска или санитайзер<br>
    </p>
    <p style="color: #000;">Параметры метода: X - число, обозначающее отклонение по горизонтали относительно позиции персонажа, Y - отклонение по вертикали. <strong style="color: #000;">Значениями параметров могут быть только числа из диапазона -3 до 3</strong>.
Отсчет координат идет <strong style="color: #000;">слева направо (X)</strong> и <strong style="color: #000;">сверху вниз (Y)</strong>. Например координата (1, -1) относительно персонажа находится справа вверху.</p>

* ```python
    player.put_on_mask()
    ```
    <p style="color: #000;">Надеть маску.</p>

* ```python
    player.wash_hands()
    ```
    <p style="color: #000;">Помыть руки.</p>

* ```python
    player.get_products()
    ```
    <p style="color: #000;">Купить продукты.</p>
    
* ```python
    player.disinfect(direction)
    ```
    <p style="color: #000;">Продезинфицировать клетку в направлении direction, где direction - число от 0 до 7, обозначающее клетку вокруг игрока. 0 - клетка сверху от персонажа, 1 - клетка справа вверху от персонажа и так далее по часовой стрелке.</p>

<p style="color: #000;">Каждый из вышеперечисленных методов занимает 1 игровой ход.</p>

#### <span style="color: #000;">Пример 1</span>
<span style="color: #000;">Следующий код передвинет персонажа на две клетки вправо и на одну клетку вверх:</span>
```python
import player

player.go_right(2)
player.go_up()
```

#### <span style="color: #000;">Пример 2</span>
<span style="color: #000;">Следующий код проверяет наличие маски или санитайзера на клетке слева от персонажа: player.look(-1, 0) == 4. При выполнении этого условия персонаж перейдёт на одну клетку влево:</span>
```python
import player

if player.look(-1, 0) == 4:
    player.go_left()
```

#### <span style="color: #000;">Пример 3</span>
<span style="color: #000;">Следующий код проверяет отсутствие вирусов на клетках справа внизу ([1 , 1]) и справа вверху ([1, -1]) от персонажа. При выполнении этих условий персонаж перейдёт на одну клетку вправо, иначе подождёт один ход:</span>
```python
import player

objects_around = player.look([1, 1], [1, -1])
if (objects_around[0] != 2 
    and objects_around[1] != 2):
        player.go_right()
else:
    player.wait()
    ...
```

#### <span style="color: #000;">Пример 4</span>
<span style="color: #000;">Следующий код проверяет наличие движущегося вверх вируса слева внизу от персонажа (player.look(-1, 1) == 2) и уничтожает его на второй ход (так как первый ход был потрачен на вызов метода player.look) - player.disinfect(7):</span>
```python
import player

if player.look(-1, 1) == 2:
    player.disinfect(7)
```
