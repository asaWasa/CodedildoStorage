## Прототип (Prototype)

Паттерн Прототип применяется для создания нового объекта путем клонирования исходного с последующей модификацией клона.
### Пример 1:
```python
import copy


class Prototype(object):
    def __init__(self):
        self._objects = {}

    def register(self, name, obj):
        self._objects[name] = obj

    def unregister(self, name):
        del self._objects[name]

    def clone(self, name, attrs):
        obj = copy.deepcopy(self._objects[name])
        obj.__dict__.update(attrs)
        return obj


class Bird(object):
    """Птица"""


prototype = Prototype()
prototype.register('bird', Bird())

owl = prototype.clone('bird', {'name': 'Owl'})
print type(owl), owl.name  # <class '__main__.Bird'> Owl

duck = prototype.clone('bird', {'name': 'Duck'})
print type(duck), duck.name  # <class '__main__.Bird'> Duck
```

### Пример 2:
```python
class Point:
    __slots__ = ('x', 'y',)

    def __init__(self, x, y):
        self.x = x
        self.y = y

# При таком классическом определении класса Point создать новую точку можно 7 способами

def make_object(cls, *args, **kwargs):
    return cls(*args, **kwargs)

point1 = Point(1, 2)
point2 = eval('{}({}, {})'.format('Point', 2, 4)) # Опасно
point3 = getattr(sys.modules[__name__], 'Point')(3, 6)
point4 = globals()['Point'](4, 8)
point5 = make_object(Point, 5, 10)
point6 = copy.deepcopy(point5)
point6.x = 6
point6.y = 12
point7 = point1.__class__(7, 14)
```

При создании point6 используется классический подход на основе прототипа: сначала мы клонируем существующий объект, а затем  инициализируем и конфигурируем его. Для создания point7 мы берем объект класса точки point1 и передаем ему другие аргументы.

На примере point6 мы видим, что в Python уже встроена поддержка прототипов в виде функции copy.deepcopy(). Однако пример point7 показывает, что в Python есть средства и получше: вместо того чтобы клонировать существующий объект и модифицировать клон, Python предоставляет доступ к объекту класса имеющегося объекта и таким образом мы можем создать новый объект непосредственно, что гораздо эффективнее клонирования.

Прототип - паттерн, порождающий объекты. Задает виды создаваемых объектов с помощью экземпляра-прототипа и создает новые объекты путем копирования этого прототипа.

```python

class Prototype:

    value = 'default'

    def clone(self, **attrs):
        """Clone a prototype and update inner attributes dictionary"""
        # Python in Practice, Mark Summerfield
        obj = self.__class__()
        obj.__dict__.update(attrs)
        return obj


class PrototypeDispatcher:
    def __init__(self):
        self._objects = {}

    def get_objects(self):
        """Get all objects"""
        return self._objects

    def register_object(self, name, obj):
        """Register an object"""
        self._objects[name] = obj

    def unregister_object(self, name):
        """Unregister an object"""
        del self._objects[name]


def main():
    """
    >>> dispatcher = PrototypeDispatcher()
    >>> prototype = Prototype()
    >>> d = prototype.clone()
    >>> a = prototype.clone(value='a-value', category='a')
    >>> b = prototype.clone(value='b-value', is_checked=True)
    >>> dispatcher.register_object('objecta', a)
    >>> dispatcher.register_object('objectb', b)
    >>> dispatcher.register_object('default', d)
    >>> [{n: p.value} for n, p in dispatcher.get_objects().items()]
    [{'objecta': 'a-value'}, {'objectb': 'b-value'}, {'default': 'default'}]
    """


if __name__ == '__main__':
    import doctest
    doctest.testmod()
```
