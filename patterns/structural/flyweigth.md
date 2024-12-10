## Приспособленец (Flyweight)

Приспособленец предназначен для обработки большого числа сравнительно небольших объектов, когда многие из этих объектов являются дубликатами. Реализация паттерна предполагает, что каждый уникальный объект представляется всего один раз и именно этот экземпляр отдается на запрос. В Python легко реализуется через словарь.

В Python подход к реализации приспособленцев естественный - благодаря наличию ссылок на объекты. Например, если бы у нас был длинный список строк, в котором много дубликатов, то, сохраняя ссылки на объекты (то есть переменные), а не литеральные строки, мы бы могли существенно сэкономить память

### Пример 1:
```python
red, green, blue = 'red', 'green', 'blue'
x = (red, green, blue, red, green, blue, green)
```

### Пример 2:
```python
import weakref


class Card:
    """The Flyweight"""

    # Could be a simple dict.
    # With WeakValueDictionary garbage collection can reclaim the object
    # when there are no other references to it.
    _pool = weakref.WeakValueDictionary()

    def __new__(cls, value, suit):
        # If the object exists in the pool - just return it
        obj = cls._pool.get(value + suit)
        # otherwise - create new one (and add it to the pool)
        if obj is None:
            obj = object.__new__(Card)
            cls._pool[value + suit] = obj
            # This row does the part we usually see in `__init__`
            obj.value, obj.suit = value, suit
        return obj

    # If you uncomment `__init__` and comment-out `__new__` -
    #   Card becomes normal (non-flyweight).
    # def __init__(self, value, suit):
    #     self.value, self.suit = value, suit

    def __repr__(self):
        return "<Card: {}{}>".format(self.value, self.suit)


def main():
    """
    >>> c1 = Card('9', 'h')
    >>> c2 = Card('9', 'h')
    >>> c1, c2
    (<Card: 9h>, <Card: 9h>)
    >>> c1 == c2
    True
    >>> c1 is c2
    True
    >>> c1.new_attr = 'temp'
    >>> c3 = Card('9', 'h')
    >>> hasattr(c3, 'new_attr')
    True
    >>> Card._pool.clear()
    >>> c4 = Card('9', 'h')
    >>> hasattr(c4, 'new_attr')
    False
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

### Пример 3:
```python
import weakref


class Color(object):
    """Приспособленец"""
    def __init__(self, name):
        self._name = name

    def __str__(self):
        return self._name


class ColorFactory(object):
    """Фабрика приспособленцев"""
    _colors = weakref.WeakValueDictionary()

    @classmethod
    def get_color(cls, name):
        value = cls._colors.get(name)
        if value is None:
            value = Color(name)
            cls._colors[name] = value
        return value


class Placemark(object):
    """Метка на карте"""
    def __init__(self, latitude, longitude, color_name):
        # координаты - внутреннее состояние (т.к. они уникальны для каждой метки)
        self._latitude = latitude
        self._longitude = longitude
        # цвет - внешнее состояние которое может быть общим у разных меток
        self._color = ColorFactory.get_color(color_name)

    def __str__(self):
        args = (self._color, self._latitude, self._longitude)
        return 'Цвет: %s; Координаты: (%0.4f, %0.4f)' % args


plmrk0 = Placemark(-74.007121, 40.714551, 'green')  # Нью-Йорк
plmrk1 = Placemark(37.617761, 55.755773, 'green')  # Москва

print plmrk0  # Цвет: green; Координаты: (-74.0071, 40.7146)
print plmrk1  # Цвет: green; Координаты: (37.6178, 55.7558)
print plmrk0._color is plmrk1._color  # True
```
