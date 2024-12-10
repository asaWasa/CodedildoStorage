## Заместитель (Proxy)

Паттерн Заместитель применяется когда мы хотим подставить один объект вместо другого. В книге "Паттерны проектирования" описаны 4 таких случая:

1. удаленный прокси, когда доступ к удаленному объекту проксируется локальным объектом;
2. виртуальный прокси, который позволяет создавать облегченные объекты вместо тяжеловесных, а последние создавать только когда это необходимо;
3. защитный прокси, который предоставляет различные уровни доступа, в зависимости от прав клиента;
4. интеллектуальная ссылка, которая выполняет "дополнительные действия при обращении к объекту" (можно также реализовать с помощью дескриптора @property)

Mock - пример реализации паттерна Заместитель
### Пример 1:
```python
"""
*TL;DR
Provides an interface to resource that is expensive to duplicate.
"""

import time


class SalesManager:
    def talk(self):
        print("Sales Manager ready to talk")


class Proxy:
    def __init__(self):
        self.busy = 'No'
        self.sales = None

    def talk(self):
        print("Proxy checking for Sales Manager availability")
        if self.busy == 'No':
            self.sales = SalesManager()
            time.sleep(0.1)
            self.sales.talk()
        else:
            time.sleep(0.1)
            print("Sales Manager is busy")


class NoTalkProxy(Proxy):
    def talk(self):
        print("Proxy checking for Sales Manager availability")
        time.sleep(0.1)
        print("This Sales Manager will not talk to you", "whether he/she is busy or not")


if __name__ == '__main__':
    p = Proxy()
    p.talk()
    p.busy = 'Yes'
    p.talk()
    p = NoTalkProxy()
    p.talk()
    p.busy = 'Yes'
    p.talk()

# OUTPUT #
# Proxy checking for Sales Manager availability
# Sales Manager ready to talk
# Proxy checking for Sales Manager availability
# Sales Manager is busy
# Proxy checking for Sales Manager availability
# This Sales Manager will not talk to you whether he/she is busy or not
# Proxy checking for Sales Manager availability
# This Sales Manager will not talk to you whether he/she is busy or not
```

### Пример 2:
```python
from functools import partial


class ImageBase(object):
    """Абстрактное изображение"""
    @classmethod
    def create(cls, width, height):
        """Создает изображение"""
        return cls(width, height)

    def draw(self, x, y, color):
        """Рисует точку заданным цветом"""
        raise NotImplementedError()

    def fill(self, color):
        """Заливка цветом"""
        raise NotImplementedError()

    def save(self, filename):
        """Сохраняет изображение в файл"""
        raise NotImplementedError()


class Image(ImageBase):
    """Изображение"""
    def __init__(self, width, height):
        self._width = int(width)
        self._height = int(height)

    def draw(self, x, y, color):
        print 'Рисуем точку; координаты: (%d, %d); цвет: %s' % (x, y, color)

    def fill(self, color):
        print 'Заливка цветом %s' % color

    def save(self, filename):
        print 'Сохраняем изображение в файл %s' % filename


class ImageProxy(ImageBase):
    """
    Заместитель изображения.
    Откладывает выполнение операций над изображением до момента его сохранения.
    """
    def __init__(self, *args, **kwargs):
        self._image = Image(*args, **kwargs)
        self.operations = []

    def draw(self, *args):
        func = partial(self._image.draw, *args)
        self.operations.append(func)

    def fill(self, *args):
        func = partial(self._image.fill, *args)
        self.operations.append(func)

    def save(self, filename):
        # выполняем все операции над изображением
        map(lambda f: f(), self.operations)
        # сохраняем изображение
        self._image.save(filename)


img = ImageProxy(200, 200)
img.fill('gray')
img.draw(0, 0, 'green')
img.draw(0, 1, 'green')
img.draw(1, 0, 'green')
img.draw(1, 1, 'green')
img.save('image.png')

# Заливка цветом gray
# Рисуем точку; координаты: (0, 0); цвет: green
# Рисуем точку; координаты: (0, 1); цвет: green
# Рисуем точку; координаты: (1, 0); цвет: green
# Рисуем точку; координаты: (1, 1); цвет: green
# Сохраняем изображение в файл image.png
```