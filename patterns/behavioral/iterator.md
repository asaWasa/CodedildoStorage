## Итератор (Iterator)

Паттерн Итератор позволяет последовательно обойти элементы коллекции или агрегированного объекта, не раскрывая деталей их внутреннего устройства. Он настолько полезен, что в Python встроена его поддержка, а кроме того, предоставляются специальные методы, которые мы можем реализовать в собственных классах, чтобы органично поддержать итерирование.

Итерирование можно поддержать тремя способами: следуя протоколу последовательности, пользуясь вариантом встроенной функции iter() с двумя аргументами или следуя протоколу итератора.

### Пример 1:
```python
class Bag:

    def __init__(self, items=None):
        self.__bag = {}
        if items is not None:
            for item in items:
                self.add(item)


    def clear(self):
        self.__bag.clear()


    def add(self, item):
        self.__bag[item] = self.__bag.get(item, 0) + 1


    def __delitem__(self, item):
        if self.__bag.get(item) is not None:
            self.__bag[item] -= 1
            if self.__bag[item] <= 0:
                del self.__bag[item]
        else:
            raise KeyError(str(item))


    def count(self, item):
        return self.__bag.get(item, 0)


    def __len__(self):
        return sum(count for count in self.__bag.values())


    def __iter__(self):
        return (item for item, count in self.__bag.items()
                for _ in range(count))


    items = __iter__


    def __contains__(self, item):
        return item in self.__bag
```

### Пример 2:
```python
class IteratorBase(object):
    """Базовый класс итератора"""
    def first(self):
        """Возвращает первый элемент коллекции.
        Если элемента не существует возбуждается исключение IndexError."""
        raise NotImplementedError()

    def last(self):
        """Возвращает последний элемент коллекции.
        Если элемента не существует возбуждается исключение IndexError."""
        raise NotImplementedError()

    def next(self):
        """Возвращает следующий элемент коллекции"""
        raise NotImplementedError()

    def prev(self):
        """Возвращает предыдущий элемент коллекции"""
        raise NotImplementedError()

    def current_item(self):
        """Возвращает текущий элемент коллекции"""
        raise NotImplementedError()

    def is_done(self, index):
        """Возвращает истину если элемент с указанным индексом существует, иначе ложь"""
        raise NotImplementedError()

    def get_item(self, index):
        """Возвращает элемент коллекции с указанным индексом, иначе возбуждает исключение IndexError"""
        raise NotImplementedError()


class Iterator(IteratorBase):
    def __init__(self, list_=None):
        self._list = list_ or []
        self._current = 0

    def first(self):
        return self._list[0]

    def last(self):
        return self._list[-1]

    def current_item(self):
        return self._list[self._current]

    def is_done(self, index):
        last_index = len(self._list) - 1
        return 0 <= index <= last_index

    def next(self):
        self._current += 1
        if not self.is_done(self._current):
            self._current = 0
        return self.current_item()

    def prev(self):
        self._current -= 1
        if not self.is_done(self._current):
            self._current = len(self._list) - 1
        return self.current_item()

    def get_item(self, index):
        if not self.is_done(index):
            raise IndexError('Нет элемента с индексом: %d' % index)
        return self._list[index]


it = Iterator(['one', 'two', 'three', 'four', 'five'])
print [it.prev() for i in range(5)]  # ['five', 'four', 'three', 'two', 'one']
print [it.next() for i in range(5)]  # ['two', 'three', 'four', 'five', 'one']
```