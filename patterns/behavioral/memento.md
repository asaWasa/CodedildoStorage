## Хранитель (Memento)

Паттерн хранитель служит для сохранения и восстановления состояния объекта, не нарушая инкапсуляцию.

В языке Python имеется готовая поддержка этого паттерна; с помощью модуля `pickle` мы можем сериализовать и десериализовать произвольные объекты Python (с некоторыми ограничениями, например, нельзя сериализовать файловый объект).

Даже в тех редких случаях, когда мы сталкиваемся с ограничением сериализации, всегда можно добавить собственную поддержку этого механизма, например, реализовав специальные методы `__getstate__()` и `__setstate__()` и, возможно, метод `__getnewargs__()`. Аналогично если мы захотим использовать формат JSON для своих классов, то сможем расширить кодировщик и декодировщик модуля `json`.

Можно было бы придумать собственный формат и протоколы, но смысла в это немного, так как Python и так предоставляет развитую поддержку этого паттерна.

### Пример 1:
```python
from copy import copy
from copy import deepcopy


def memento(obj, deep=False):
    state = deepcopy(obj.__dict__) if deep else copy(obj.__dict__)

    def restore():
        obj.__dict__.clear()
        obj.__dict__.update(state)

    return restore


class Transaction:
    """A transaction guard.
    This is, in fact, just syntactic sugar around a memento closure.
    """

    deep = False
    states = []

    def __init__(self, deep, *targets):
        self.deep = deep
        self.targets = targets
        self.commit()

    def commit(self):
        self.states = [memento(target, self.deep) for target in self.targets]

    def rollback(self):
        for a_state in self.states:
            a_state()


class Transactional:
    """Adds transactional semantics to methods. Methods decorated  with
    @Transactional will rollback to entry-state upon exceptions.
    """

    def __init__(self, method):
        self.method = method

    def __get__(self, obj, T):
        def transaction(*args, **kwargs):
            state = memento(obj)
            try:
                return self.method(obj, *args, **kwargs)
            except Exception as e:
                state()
                raise e

        return transaction


class NumObj:
    def __init__(self, value):
        self.value = value

    def __repr__(self):
        return '<%s: %r>' % (self.__class__.__name__, self.value)

    def increment(self):
        self.value += 1

    @Transactional
    def do_stuff(self):
        self.value = '1111'  # <- invalid value
        self.increment()  # <- will fail and rollback


def main():
    """
    >>> num_obj = NumObj(-1)
    >>> print(num_obj)
    <NumObj: -1>
    >>> a_transaction = Transaction(True, num_obj)
    >>> try:
    ...    for i in range(3):
    ...        num_obj.increment()
    ...        print(num_obj)
    ...    a_transaction.commit()
    ...    print('-- committed')
    ...    for i in range(3):
    ...        num_obj.increment()
    ...        print(num_obj)
    ...    num_obj.value += 'x'  # will fail
    ...    print(num_obj)
    ... except Exception:
    ...    a_transaction.rollback()
    ...    print('-- rolled back')
    <NumObj: 0>
    <NumObj: 1>
    <NumObj: 2>
    -- committed
    <NumObj: 3>
    <NumObj: 4>
    <NumObj: 5>
    -- rolled back
    >>> print(num_obj)
    <NumObj: 2>
    >>> print('-- now doing stuff ...')
    -- now doing stuff ...
    >>> try:
    ...    num_obj.do_stuff()
    ... except Exception:
    ...    print('-> doing stuff failed!')
    ...    import sys
    ...    import traceback
    ...    traceback.print_exc(file=sys.stdout)
    -> doing stuff failed!
    Traceback (most recent call last):
    ...
    TypeError: ...str...int...
    >>> print(num_obj)
    <NumObj: 2>
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

### Пример 2:
```python
class Memento(object):
    """Хранитель"""
    def __init__(self, state):
        self._state = state

    def get_state(self):
        return self._state


class Caretaker(object):
    """Опекун"""
    def __init__(self):
        self._memento = None

    def get_memento(self):
        return self._memento

    def set_memento(self, memento):
        self._memento = memento


class Originator(object):
    """Создатель"""
    def __init__(self):
        self._state = None

    def set_state(self, state):
        self._state = state

    def get_state(self):
        return self._state

    def save_state(self):
        return Memento(self._state)

    def restore_state(self, memento):
        self._state = memento.get_state()


originator = Originator()
caretaker = Caretaker()

originator.set_state('on')
print 'Originator state:', originator.get_state()  # Originator state: on
caretaker.set_memento(originator.save_state())

originator.set_state('off')
print 'Originator change state:', originator.get_state()  # Originator change state: off

originator.restore_state(caretaker.get_memento())
print 'Originator restore state:', originator.get_state()  # Originator restore state: on
```