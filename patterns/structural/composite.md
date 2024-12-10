## Компоновщик (Composite)

Паттерн Компоновщик позволяет единообразно обрабатывать объекты, образующие иерархию, вне зависимости от того, содержат они другие объекты или нет. Такие объекты называют составными.

В классическом решении составные объекты - как отдельные, так и коллекции - имеют один и тот же базовый класс. У составных и несоставных объектов обычно одни и те же основные методы, но составные объекты добавляют методы для поддержки добавления, удаления и перебора дочерних объектов.
### Пример 1:
```python
class Graphic:
    def render(self):
        raise NotImplementedError("You should implement this.")


class CompositeGraphic(Graphic):
    def __init__(self):
        self.graphics = []

    def render(self):
        for graphic in self.graphics:
            graphic.render()

    def add(self, graphic):
        self.graphics.append(graphic)

    def remove(self, graphic):
        self.graphics.remove(graphic)


class Ellipse(Graphic):
    def __init__(self, name):
        self.name = name

    def render(self):
        print("Ellipse: {}".format(self.name))


if __name__ == '__main__':
    ellipse1 = Ellipse("1")
    ellipse2 = Ellipse("2")
    ellipse3 = Ellipse("3")
    ellipse4 = Ellipse("4")

    graphic1 = CompositeGraphic()
    graphic2 = CompositeGraphic()

    graphic1.add(ellipse1)
    graphic1.add(ellipse2)
    graphic1.add(ellipse3)
    graphic2.add(ellipse4)

    graphic = CompositeGraphic()

    graphic.add(graphic1)
    graphic.add(graphic2)

    graphic.render()

# OUTPUT #
# Ellipse: 1
# Ellipse: 2
# Ellipse: 3
# Ellipse: 4
```

### Пример 2:
```python
# Класс представляющий одновременно примитивы и контейнеры
class Graphic(object):
    def draw(self):
        raise NotImplementedError()

    def add(self, obj):
        raise NotImplementedError()

    def remove(self, obj):
        raise NotImplementedError()

    def get_child(self, index):
        raise NotImplementedError()


class Line(Graphic):
    def draw(self):
        print 'Линия'


class Rectangle(Graphic):
    def draw(self):
        print 'Прямоугольник'


class Text(Graphic):
    def draw(self):
        print 'Текст'


class Picture(Graphic):
    def __init__(self):
        self._children = []

    def draw(self):
        print 'Изображение'
        # вызываем отрисовку у вложенных объектов
        for obj in self._children:
            obj.draw()

    def add(self, obj):
        if isinstance(obj, Graphic) and not obj in self._children:
            self._children.append(obj)

    def remove(self, obj):
        index = self._children.index(obj)
        del self._children[index]

    def get_child(self, index):
        return self._children[index]


pic = Picture()
pic.add(Line())
pic.add(Rectangle())
pic.add(Text())
pic.draw()
# Изображение
# Линия
# Прямоугольник
# Текст

line = pic.get_child(0)
line.draw()  # Линия
```