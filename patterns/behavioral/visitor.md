## Посетитель (Visitor)

Паттерн Посетитель используется, когда нужно применить некую функцию к каждому элементу коллекции или объекту-агрегатору. Это не то же самое, что типичное использование паттерна Итератор - где мы обходим коллекцию или агрегат и вызываем некий метод для каждого элемента, - поскольку в случае "посетителя" вызывается внешнняя функция, а не метод.

В Python имеется встроенная поддержва этого паттерна. Например конструкция `new_list = map(function, old_sequence)` означает, что `function()` вызывается для каждого элемента `old_sequence`, в результате чего порождается `new_list`

### Пример 1:
```python
class FruitVisitor(object):
    """Посетитель"""
    def draw(self, fruit):
        methods = {
            Apple: self.draw_apple,
            Pear: self.draw_pear,
        }
        draw = methods.get(type(fruit), self.draw_unknown)
        draw(fruit)

    def draw_apple(self, fruit):
        print 'Яблоко'

    def draw_pear(self, fruit):
        print 'Груша'

    def draw_unknown(self, fruit):
        print 'Фрукт'


class Fruit(object):
    """Фрукты"""
    def draw(self, visitor):
        visitor.draw(self)


class Apple(Fruit):
    """Яблоко"""


class Pear(Fruit):
    """Груша"""


class Banana(Fruit):
    """Банан"""


visitor = FruitVisitor()

apple = Apple()
apple.draw(visitor)
# Яблоко

pear = Pear()
pear.draw(visitor)
# Груша

banana = Banana()
banana.draw(visitor)
# Фрукт
```

### Пример 2:
```python
class Node:
    pass


class A(Node):
    pass


class B(Node):
    pass


class C(A, B):
    pass


class Visitor:
    def visit(self, node, *args, **kwargs):
        meth = None
        for cls in node.__class__.__mro__:
            meth_name = 'visit_' + cls.__name__
            meth = getattr(self, meth_name, None)
            if meth:
                break

        if not meth:
            meth = self.generic_visit
        return meth(node, *args, **kwargs)

    def generic_visit(self, node, *args, **kwargs):
        print('generic_visit ' + node.__class__.__name__)

    def visit_B(self, node, *args, **kwargs):
        print('visit_B ' + node.__class__.__name__)


def main():
    """
    >>> a, b, c = A(), B(), C()
    >>> visitor = Visitor()
    >>> visitor.visit(a)
    generic_visit A
    >>> visitor.visit(b)
    visit_B B
    >>> visitor.visit(c)
    visit_B C
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

