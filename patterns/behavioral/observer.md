## Наблюдатель (Observer)

Паттерн Наблюдатель поддерживает отношения зависимости многие-ко-многим между объектами, например, когда изменяется состояние одного объекта, уведомляются все связанные с ним объекты. В наши дни, наверное самый распространенный пример этого паттерна и его вариантов - парадигма модель-представление-контроллер (MVC). В этой парадигме модель описывает данные, одно или несколько предствалений эти данные визиалируют, а одни или несколько контроллеров осуществляют посредничество между вводом (например, взаимодействие с пользователем) и моделью. И любые изменения в модели автоматически отражаются в ассоциированных с ней представлениях.

У подхода MVC есть одно популярное упрощение - использовать только модели и представления, но поручить представлениям как визуализацию данных, так и передачу модели входных данных; иными словами, представления совмещены с контроллерами. В терминах паттерна Наблюдатель это означает, что представления - наблюдатели, а модель - наблюдаемый объект.

В качестве примеров можно назвать триггеры в базах данных, систему сигнализации Django, механизм сигналов и слотов в библиотеке QT и многочисленные применения технологии WebSockets.

### Пример 1: 
```python
class Subject:
    def __init__(self):
        self._observers = []

    def attach(self, observer):
        if observer not in self._observers:
            self._observers.append(observer)

    def detach(self, observer):
        try:
            self._observers.remove(observer)
        except ValueError:
            pass

    def notify(self, modifier=None):
        for observer in self._observers:
            if modifier != observer:
                observer.update(self)


class Data(Subject):
    def __init__(self, name=''):
        Subject.__init__(self)
        self.name = name
        self._data = 0

    @property
    def data(self):
        return self._data

    @data.setter
    def data(self, value):
        self._data = value
        self.notify()


class HexViewer:
    def update(self, subject):
        print('HexViewer: Subject {} has data 0x{:x}'.format(subject.name, subject.data))


class DecimalViewer:
    def update(self, subject):
        print('DecimalViewer: Subject %s has data %d' % (subject.name, subject.data))


def main():
    """
    >>> data1 = Data('Data 1')
    >>> data2 = Data('Data 2')
    >>> view1 = DecimalViewer()
    >>> view2 = HexViewer()
    >>> data1.attach(view1)
    >>> data1.attach(view2)
    >>> data2.attach(view2)
    >>> data2.attach(view1)
    >>> data1.data = 10
    DecimalViewer: Subject Data 1 has data 10
    HexViewer: Subject Data 1 has data 0xa
    >>> data2.data = 15
    HexViewer: Subject Data 2 has data 0xf
    DecimalViewer: Subject Data 2 has data 15
    >>> data1.data = 3
    DecimalViewer: Subject Data 1 has data 3
    HexViewer: Subject Data 1 has data 0x3
    >>> data2.data = 5
    HexViewer: Subject Data 2 has data 0x5
    DecimalViewer: Subject Data 2 has data 5
    # Detach HexViewer from data1 and data2
    >>> data1.detach(view2)
    >>> data2.detach(view2)
    >>> data1.data = 10
    DecimalViewer: Subject Data 1 has data 10
    >>> data2.data = 15
    DecimalViewer: Subject Data 2 has data 15
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

### Пример 2:
```python
class Subject(object):
    """Субъект"""
    def __init__(self):
        self._data = None
        self._observers = set()

    def attach(self, observer):
        # подписаться на оповещение
        if not isinstance(observer, ObserverBase):
            raise TypeError()
        self._observers.add(observer)

    def detach(self, observer):
        # отписаться от оповещения
        self._observers.remove(observer)

    def get_data(self):
        return self._data

    def set_data(self, data):
        self._data = data
        self.notify(data)

    def notify(self, data):
        # уведомить всех наблюдателей о событии
        for observer in self._observers:
            observer.update(data)


class ObserverBase(object):
    """Абстрактный наблюдатель"""
    def update(self, data):
        raise NotImplementedError()


class Observer(ObserverBase):
    """Наблюдатель"""
    def __init__(self, name):
        self._name = name

    def update(self, data):
        print '%s: %s' % (self._name, data)


subject = Subject()
subject.attach(Observer('Наблюдатель 1'))
subject.attach(Observer('Наблюдатель 2'))
subject.set_data('данные для наблюдателя')
# Наблюдатель 2: данные для наблюдателя
# Наблюдатель 1: данные для наблюдателя
```