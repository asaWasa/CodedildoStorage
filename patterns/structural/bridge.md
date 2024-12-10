## Мост (Bridge)

***Мост (Bridge)*** - паттерн, структурирующий объекты. Основная задача - отделить абстракцию от её реализации так, чтобы то и другое можно было изменять независимо.

Традиционный подход без использования паттерна Мост состоит в том, чтобы создать один или несколько абстрактных базовых классов, а затем предоставить две или более конкретных реализации каждого базового класса.
А паттерн Мост предлагает создать две независимых иерархии классов: "абстрактную", которая определяет операции (например интерфейс или алгоритм верхнего уровня) и конкретную, предоставляющую реализацию, которые в конечном итоге и будут вызваны из абстрактных операций. "Абстрактный" класс агрегирует экземпляр одного из конкретных классов с реализацией - и этот последний служит *мостом* между абстрактным интерфейсом и конкретными операциями.

### Пример 1:
```python
# ConcreteImplementor 1/2
class DrawingAPI1:
    def draw_circle(self, x, y, radius):
        print('API1.circle at {}:{} radius {}'.format(x, y, radius))


# ConcreteImplementor 2/2
class DrawingAPI2:
    def draw_circle(self, x, y, radius):
        print('API2.circle at {}:{} radius {}'.format(x, y, radius))


# Refined Abstraction
class CircleShape:
    def __init__(self, x, y, radius, drawing_api):
        self._x = x
        self._y = y
        self._radius = radius
        self._drawing_api = drawing_api

    # low-level i.e. Implementation specific
    def draw(self):
        self._drawing_api.draw_circle(self._x, self._y, self._radius)

    # high-level i.e. Abstraction specific
    def scale(self, pct):
        self._radius *= pct


def main():
    """
    >>> shapes = (CircleShape(1, 2, 3, DrawingAPI1()), CircleShape(5, 7, 11, DrawingAPI2()))
    >>> for shape in shapes:
    ...    shape.scale(2.5)
    ...    shape.draw()
    API1.circle at 1:2 radius 7.5
    API2.circle at 5:7 radius 27.5
    """


if __name__ == '__main__':
    import doctest
    doctest.testmod()
```

### Пример 2:
```python
class TVBase(object):
    """Абстрактный телевизор"""
    def tune_channel(self, channel):
        raise NotImplementedError()


class SonyTV(TVBase):
    """Телевизор Sony"""
    def tune_channel(self, channel):
        print('Sony TV: выбран %d канал' % channel)


class SharpTV(TVBase):
    """Телевизор Sharp"""
    def tune_channel(self, channel):
        print('Sharp TV: выбран %d канал' % channel)


class RemoteControlBase(object):
    """Абстрактный пульт управления"""
    def __init__(self):
        self._tv = self.get_tv()

    def get_tv(self):
        raise NotImplementedError()

    def tune_channel(self, channel):
        self._tv.tune_channel(channel)


class RemoteControl(RemoteControlBase):
    """Пульт управления"""
    def __init__(self):
        super(RemoteControl, self).__init__()
        self._channel = 0  # текущий канал

    def get_tv(self):
        return SharpTV()

    def tune_channel(self, channel):
        super(RemoteControl, self).tune_channel(channel)
        self._channel = channel

    def next_channel(self):
        self._channel += 1
        self.tune_channel(self._channel)

    def previous_channel(self):
        self._channel -= 1
        self.tune_channel(self._channel)


remote_control = RemoteControl()
remote_control.tune_channel(5)  # Sharp TV: выбран 5 канал
remote_control.next_channel()  # Sharp TV: выбран 6 канал
```