## Фасад (Facade)

Паттерн Фасад служит для того, чтобы предоставить упрощенный унифицированный интерфейс к подсистеме, чей истинный интерфейс слишком сложен или написан на таком низком уровне, что работать с ним неудобно. Фасад определяет интерфейс более высокого уровня, который упрощает использование подсистемы.

В стандартной библиотеке Python имеется несколько модулей для работы с сжатыми файлами - gzip, tar+gzip, zip. Все они имеют разные интерфейсы. Если мы хотим иметь один унифицированный интерфейс для работы с архивами, мы можем воспользоваться паттерном Фасад.

Паттерны Фасад и [Адаптер](adapter.md) на первый взгляд кажутся похожими. Разница в том, что Фасад надстраивает простой интерфейс поверх сложного, а Адаптер надстраивает унифицированный интерфейс над каким-то другим (необязательно сложным). Оба эти паттерна можно использовать совместно. Например определить интерфейс для работы с архивными файлами, написать адаптер для каждого формата и надстроить поверх них фасад, чтобы пользователям не нужно было беспокоиться о том, какой конкретно формат файла используется.

### Пример 1:
```python
# Complex computer parts
class CPU:
    """
    Simple CPU representation.
    """
    def freeze(self):
        print("Freezing processor.")

    def jump(self, position):
        print("Jumping to:", position)

    def execute(self):
        print("Executing.")


class Memory:
    """
    Simple memory representation.
    """
    def load(self, position, data):
        print("Loading from {0} data: '{1}'.".format(position, data))


class SolidStateDrive:
    """
    Simple solid state drive representation.
    """
    def read(self, lba, size):
        return "Some data from sector {0} with size {1}".format(lba, size)


class ComputerFacade:
    """
    Represents a facade for various computer parts.
    """
    def __init__(self):
        self.cpu = CPU()
        self.memory = Memory()
        self.ssd = SolidStateDrive()

    def start(self):
        self.cpu.freeze()
        self.memory.load("0x00", self.ssd.read("100", "1024"))
        self.cpu.jump("0x00")
        self.cpu.execute()


def main():
    """
    >>> computer_facade = ComputerFacade()
    >>> computer_facade.start()
    Freezing processor.
    Loading from 0x00 data: 'Some data from sector 100 with size 1024'.
    Jumping to: 0x00
    Executing.
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

### Пример 2:
```python
class Paper(object):
    """Бумага"""
    def __init__(self, count):
        self._count = count

    def get_count(self):
        return self._count

    def draw(self, text):
        if self._count > 0:
            self._count -= 1
            print text


class Printer(object):
    """Принтер"""
    def error(self, msg):
        print 'Ошибка: %s' % msg

    def print_(self, paper, text):
        if paper.get_count() > 0:
            paper.draw(text)
        else:
            self.error('Бумага закончилась')


class Facade(object):
    def __init__(self):
        self._printer = Printer()
        self._paper = Paper(1)

    def write(self, text):
        self._printer.print_(self._paper, text)


f = Facade()
f.write('Hello world!')  # Hello world!
f.write('Hello world!')  # Ошибка: Бумага закончилась
```
