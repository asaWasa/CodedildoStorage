## ООП

### Инкапсуляция

*Инкапсуляция* - механизм языка, позволяющий объединить данные и методы, работающие с этими данными, в единый объект и скрыть детали реализации от пользователя.

Подлинное назначение инкапсуляции — собрать в одном месте знания, относящиеся к устройству некой сущности, правилам обращения и операциям с ней. Инкапсуляция появилась гораздо раньше, чем принято думать. Модули в программах на C — это инкапсуляция. Подпрограммы на ассемблере — это инкапсуляция. Противоположность инкапсуляции — размазывание знаний о функционировании чего-либо по всей программе.

*Пример*: работа с денежными величинами. Не секрет, что во многих e-commerce системах денежные величины реализованы в виде чисел с плавающей запятой. Думаю, все из нас в курсе, что при простом сложении двух «целых» чисел, представленных в виде переменных с плавающих запятой, может образоваться «немного не целое число». Поэтому при такой реализации там и тут приходится вставлять вызов функции округления. Это и есть размазывание знаний об устройстве сущности по всей программе. Инкапсуляция в данном случае — собрать (спрятать) в одном месте знание о том, что деньги представлены в виде величины с плавающей запятой, и что её постоянно приходится округлять при самых невинных операциях. Спрятать так, чтобы при использовании сущности «деньги» речь об округлении даже не заходила. При инкапсуляции не будет никаких проблем заменить реализацию «денег» с числа с плавающей на число с фиксированной запятой.

Можно сказать, что сокрытие – это одна из задач инкапсуляции. Но само по себе сокрытие данных инкапсуляцией не является. Также сказать, что инкапсуляция – это сокрытие данных, тоже было бы неверно. Потому что её задачи выходят за рамки сокрытия.

Если мы говорим, что данный метод инкапсулирует некий алгоритм, то подразумеваем, что в данном методе происходит определённое вычисление, детали которого нам знать необязательно, но результатам которого мы можем доверять и пользоваться ими. Также мы можем сказать, что объект, в котором инкапсулированы данные, может скрывать их – то есть защищать от несанкционированного доступа. Таким образом, разграничивать понятие инкапсуляции и сокрытия данных всё-таки нужно и важно видеть грань между ними. Инкапсуляция – технология объединения собственно данных и методов их обработки. В результате и сами данные, и алгоритмы работы с ними становятся логически неотделимы. Типичный пример из C++ – поля и методы класса.

Итак, если инкапсуляция обеспечивает своего рода целостность объекта, то сокрытие - скрывает детали о процессе. Для "настройки" доступа к данным в классе и к классу непосредственно используются так называемые модификаторы доступа. Так вот использование этих модификаторов доступа и есть сокрытие.

### Наследование

*Наследование* - механизм языка, который позволяет описывать новый класс на основе существующего. В "истинном" ООП нужно для обеспечения реализации полиморфизма, как самостоятельная единица, не нужно и даже вредно, потому что является причиной сильного связывания. Наследованию лучше предпочитать композицию.

### Полиморфизм

*Полиморфизм* имеет несколько форм:

- Специальный (Ad-Hoc) (в некоторых языках представлен механизмом перегрузки методов)
- Параметрический (в некоторых языках представлен дженериками)
- Полиморфизм подтипов (достигается с помощью механизмов наследования и апкаста). Когда говорят о полиморфизме чаще всего имеют в виду его

*Полиморфизм* - возможность схожим типам данных, которые явно заданы иерархией наследования иметь различные реализации (с помощью переопределения методов и апкаста)

Также в языках программирования и теории типов полиморфизмом называется способность функции обрабатывать данные разных типов.

### Абстракция

*Абстракция* гласит что мы должны выделять важные характеристики объекта. Мысль в том, чтобы мы могли определить минимально необходимый набор этих характеристик для того чтобы можно было решить поставленную задачу.
Часто путают с инкапсуляцией, потому что и то и другое косвенно влияет на формирование публичного интерфейса типа.
Довольно тривиальная парадигма и поэтому часто не указывается как таковая.

### Композиция 
*Композиция* — это принцип, при котором один объект создаётся как часть другого объекта.
Вместо наследования классов композиция позволяет строить сложные объекты,
объединяя простые, делая код гибким и повторно используемым.

*Например класс который внутри себя использует другой класс*

## Какие принципы программирования вы знаете

- [10 Coding principles and acronyms demystified!](https://areknawo.com/10-coding-principles-and-acronyms-demystified/)

### KISS

Принцип *Keep It Stupid Simple* («Придерживайся простоты») велит вам следить за тем, чтобы код оставался как можно более простым. Чем код проще, тем легче в нем разобраться, как вам, так и другим людям, занимающимся его поддержкой. Под простотой главным образом имеется в виду отказ от использования хитроумных приемов и ненужного усложнения.

В качестве примеров нарушения этого принципа можно назвать написание отдельной функции только лишь для осуществления операции сложения или использование побитового оператора (right shift >> 1) для деления целых чисел на 2. Последнее, безусловно, более эффективно, чем обычное (/2), но при этом очень сильно снижается понятность кода. Применяя такой подход, вы осуществляете clever coding («заумный кодинг») и over-optimization (чрезмерную оптимизацию). И то, и другое в долгосрочной перспективе не слишком хорошо сказывается на здоровье вашего кода.

### DRY

Принцип *Don’t Repeat Yourself* («Не повторяйся») напоминает нам, что каждое повторяемое поведение в коде следует обособлять (например, выделять в отдельную функцию) для возможности многократного использования. Когда у вас в кодовой базе есть два совершенно одинаковых фрагмента кода, это не хорошо. Это часто приводит к рассинхронизации и прочим багам, не говоря уже о том, что от этого увеличивается размер программы.

### YAGNI

Принцип *You Aren’t Gonna Need It* («Тебе это не понадобится») говорит о том, что нежелательно оставлять в продакшене «точки расширения» (места, предназначенные только для того, чтобы позволить вам в будущем легко добавить новый функционал). Конечно, мы не говорим о случаях, когда речь идет об уже заказанном функционале. Такие точки расширения вносят ненужную сложность и увеличивают размер вашей кодовой базы.

### SLAP

Принцип *Single Level of Abstraction Principle* («Принцип единого уровня абстракций») означает, что функции должны иметь единый уровень абстракции. Скажем, функция, читающая input, не должна также обрабатывать полученные данные. Для этого она должна задействовать отдельную функцию, находящуюся на другом, более низком уровне абстракции. Чем более общей является функция и чем больше других функций она использует, тем выше она располагается в абстракционной иерархии.

### SOLID принципы

*SOLID* - это аббревиатура от 5 принципов, описанных Робертом Мартином, которые способствуют созданию хорошего объектно-ориентированного (и не только) кода.

**S**: Single Responsibility Principle (Принцип единственной ответственности).
>Каждый класс должен решать лишь одну задачу.

**O**: Open-Closed Principle (Принцип открытости-закрытости).
>Программные сущности (классы, модули, функции) должны быть открыты для расширения, но не для модификации.

**L**: Liskov Substitution Principle (Принцип подстановки Барбары Лисков).
>Необходимо, чтобы подклассы могли бы служить заменой для своих суперклассов.

**I**: Interface Segregation Principle (Принцип разделения интерфейса).
>Создавайте узкоспециализированные интерфейсы, предназначенные для конкретного клиента. Клиенты не должны зависеть от интерфейсов, которые они не используют.

**D**: Dependency Inversion Principle (Принцип инверсии зависимостей).
>Объектом зависимости должна быть абстракция, а не что-то конкретное.

- Модули верхних уровней не должны зависеть от модулей нижних уровней. Оба типа модулей должны зависеть от абстракций.
- Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.

## Что такое code cohesion & code coupling

**Связанность модулей (coupling)**, часто называемую **зацеплением**, характеризует степень независимости модулей. При проектировании систем необходимо стремиться, чтобы модули имели минимальную зависимость друг от друга, т.е. были минимально «сцеплены» между собой (отсюда и термин «сцепление» или связанность). Это требование вытекает из одного из основных принципов системного подхода, требующего минимизации информационных потоков между подсистемами.

**Связность (cohesion)** характеризует целостность, «плотность» модуля, т.е. насколько модуль является простым с точки зрения его использования. В идеале модуль должен выполнять одну единственную функцию и иметь минимальное число «ручек управления». Примером модуля имеющего максимальную связность является модуль проверки орфографии, вычисления заработной платы сотрудника, вычисления логарифма функции. Если связанность является характеристикой системы, то связность характеризует отдельно взятый модуль.

## Какие шаблоны проектирования вы знаете

- "Марк Саммерфилд - Python на практике"
- [GitHub - pkolt/design_patterns: Паттерны проектирования](https://github.com/pkolt/design_patterns)
- [GitHub - faif/python-patterns: A collection of design patterns/idioms in Python](https://github.com/faif/python-patterns)
- [Python Design Patterns](https://python-patterns.guide/)

### Порождающие (Creational)

Порождающие паттерны проектирования описывают, как создавать объекты. Обычно объект создается путем вызова констуктора, но иногда требуется большая гибкость именно для этого порождающие паттерны и полезны.

#### Абстрактная фабрика (Abstract factory)

Предназначен для случаев, когда требуется создать сложный объект, состоящий из других объектов, причем все составляющие объекты принадлежат одному "семейству". Предоставляет интерфейс для создания семейств взаимосвязанных или взаимозависимых объектов, не специфицируя их конкретных классов.

Например, в системе с GUI может быть абстрактная фабрика виджетов, которой наследуют три конкретных фабрики: MacWidgetFactory, XfceWidgetFactory, WindowsWidgetFactory, каждая из которых предоставляет методы для создания одних и тех же объектов (make_button(), make_spinbox() и т.д), стилизованных, однако, как принято на конкретной платформе. Это дает возможность создать обобщенную функцию create_dialog(), которая принимает экземпляр фабрики в качестве аргумента и создает диалоговое окно, выглядещее как в OS X, Xfce или Windows - в зависимости от того какую фабрику мы передали.

Классы абстрактной фабрики часто реализуются фабричными методами, но могут быть реализованы и с помощью паттерна прототип.

```python
"""
*What is this pattern about?
In Java and other languages, the Abstract Factory Pattern serves to provide an interface for
creating related/dependent objects without need to specify their
actual class.
The idea is to abstract the creation of objects depending on business
logic, platform choice, etc.
In Python, the interface we use is simply a callable, which is "builtin" interface
in Python, and in normal circumstances we can simply use the class itself as
that callable, because classes are first class objects in Python.
*What does this example do?
This particular implementation abstracts the creation of a pet and
does so depending on the factory we chose (Dog or Cat, or random_animal)
This works because both Dog/Cat and random_animal respect a common
interface (callable for creation and .speak()).
Now my application can create pets abstractly and decide later,
based on my own criteria, dogs over cats.
*Where is the pattern used practically?
*References:
https://sourcemaking.com/design_patterns/abstract_factory
http://ginstrom.com/scribbles/2007/10/08/design-patterns-python-style/
*TL;DR
Provides a way to encapsulate a group of individual factories.
"""

import random


class PetShop:

    """A pet shop"""

    def __init__(self, animal_factory=None):
        """pet_factory is our abstract factory.  We can set it at will."""

        self.pet_factory = animal_factory

    def show_pet(self):
        """Creates and shows a pet using the abstract factory"""

        pet = self.pet_factory()
        print("We have a lovely {}".format(pet))
        print("It says {}".format(pet.speak()))


class Dog:
    def speak(self):
        return "woof"

    def __str__(self):
        return "Dog"


class Cat:
    def speak(self):
        return "meow"

    def __str__(self):
        return "Cat"


# Additional factories:

# Create a random animal
def random_animal():
    """Let's be dynamic!"""
    return random.choice([Dog, Cat])()


# Show pets with various factories
if __name__ == "__main__":

    # A Shop that sells only cats
    cat_shop = PetShop(Cat)
    cat_shop.show_pet()
    print("")

    # A shop that sells random animals
    shop = PetShop(random_animal)
    for i in range(3):
        shop.show_pet()
        print("=" * 20)

# OUTPUT #
# We have a lovely Cat
# It says meow
#
# We have a lovely Dog
# It says woof
# ====================
# We have a lovely Cat
# It says meow
# ====================
# We have a lovely Cat
# It says meow
# ====================
```

#### Построитель (Builder)

Построитель аналогичен паттерну Абстрактная фабрика в том смысле, что оба предназначены для создания сложных объектов, составленных из других объектов. Но отличается тем, что не только предоставляет методы для построения сложного объекта, но и хранит внутри себя его полное представление.

Этот паттерн допускает такую же композиционную структуру как и Абстрактная фабрика (то есть сложные объекты, составленные из нескольких более простых) но особенно удобен в ситуациях, когда представление составного объета должно быть отделено от алгоритмов композиции

Отделяет конструирование сложного объекта от его представления, так что в результате одного и того же процесса конструирования могут получаться разные представления. От абстрактной фабрики отличается тем, что делает акцент на пошаговом конструировании объекта. Строитель возвращает объект на последнем шаге, тогда как абстрактная фабрика возвращает объект немедленно. Строитель часто используется для создания паттерна компоновщик.

```python
"""
*What is this pattern about?
It decouples the creation of a complex object and its representation,
so that the same process can be reused to build objects from the same
family.
This is useful when you must separate the specification of an object
from its actual representation (generally for abstraction).
*What does this example do?
The first example achieves this by using an abstract base
class for a building, where the initializer (__init__ method) specifies the
steps needed, and the concrete subclasses implement these steps.
In other programming languages, a more complex arrangement is sometimes
necessary. In particular, you cannot have polymorphic behaviour in a constructor in C++ -
see https://stackoverflow.com/questions/1453131/how-can-i-get-polymorphic-behavior-in-a-c-constructor
- which means this Python technique will not work. The polymorphism
required has to be provided by an external, already constructed
instance of a different class.
In general, in Python this won't be necessary, but a second example showing
this kind of arrangement is also included.
*Where is the pattern used practically?
*References:
https://sourcemaking.com/design_patterns/builder
*TL;DR
Decouples the creation of a complex object and its representation.
"""


# Abstract Building
class Building:
    def __init__(self):
        self.build_floor()
        self.build_size()

    def build_floor(self):
        raise NotImplementedError

    def build_size(self):
        raise NotImplementedError

    def __repr__(self):
        return 'Floor: {0.floor} | Size: {0.size}'.format(self)


# Concrete Buildings
class House(Building):
    def build_floor(self):
        self.floor = 'One'

    def build_size(self):
        self.size = 'Big'


class Flat(Building):
    def build_floor(self):
        self.floor = 'More than One'

    def build_size(self):
        self.size = 'Small'


# In some very complex cases, it might be desirable to pull out the building
# logic into another function (or a method on another class), rather than being
# in the base class '__init__'. (This leaves you in the strange situation where
# a concrete class does not have a useful constructor)


class ComplexBuilding:
    def __repr__(self):
        return 'Floor: {0.floor} | Size: {0.size}'.format(self)


class ComplexHouse(ComplexBuilding):
    def build_floor(self):
        self.floor = 'One'

    def build_size(self):
        self.size = 'Big and fancy'


def construct_building(cls):
    building = cls()
    building.build_floor()
    building.build_size()
    return building


def main():
    """
    >>> house = House()
    >>> house
    Floor: One | Size: Big
    >>> flat = Flat()
    >>> flat
    Floor: More than One | Size: Small
    # Using an external constructor function:
    >>> complex_house = construct_building(ComplexHouse)
    >>> complex_house
    Floor: One | Size: Big and fancy
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

#### Фабричный метод (Factory method)

Паттерн Фабричный метод применяется, когда мы хотим, чтобы подклассы выбирали, какой класс инстанциировать, когда запрашивается объект. Это полезно само по себе, но можно пойти дальше и использовать в случае, когда класс заранее неизвестен (например, зависит от информации, прочитанной из файла или введенных пользователем данных).

Абстрактная фабрика часто реализуется с помощью фабричных методов.
Фабричные методы часто вызываются внутри шаблонных методов.

```python
"""*What is this pattern about?
A Factory is an object for creating other objects.
*What does this example do?
The code shows a way to localize words in two languages: English and
Greek. "get_localizer" is the factory function that constructs a
localizer depending on the language chosen. The localizer object will
be an instance from a different class according to the language
localized. However, the main code does not have to worry about which
localizer will be instantiated, since the method "localize" will be called
in the same way independently of the language.
*Where can the pattern be used practically?
The Factory Method can be seen in the popular web framework Django:
http://django.wikispaces.asu.edu/*NEW*+Django+Design+Patterns For
example, in a contact form of a web page, the subject and the message
fields are created using the same form factory (CharField()), even
though they have different implementations according to their
purposes.
*References:
http://ginstrom.com/scribbles/2007/10/08/design-patterns-python-style/
*TL;DR
Creates objects without having to specify the exact class.
"""


class GreekLocalizer:
    """A simple localizer a la gettext"""

    def __init__(self):
        self.translations = {"dog": "σκύλος", "cat": "γάτα"}

    def localize(self, msg):
        """We'll punt if we don't have a translation"""
        return self.translations.get(msg, msg)


class EnglishLocalizer:
    """Simply echoes the message"""

    def localize(self, msg):
        return msg


def get_localizer(language="English"):
    """Factory"""
    localizers = {
        "English": EnglishLocalizer,
        "Greek": GreekLocalizer,
    }
    return localizers[language]()


def main():
    """
    # Create our localizers
    >>> e, g = get_localizer(language="English"), get_localizer(language="Greek")
    # Localize some text
    >>> for msg in "dog parrot cat bear".split():
    ...     print(e.localize(msg), g.localize(msg))
    dog σκύλος
    parrot parrot
    cat γάτα
    bear bear
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

#### Прототип (Prototype)

Паттерн Прототип применяется для создания нового объекта путем клонирования исходного с последующей модификацией клона.

Способы создания нового объекта в Python:

```python
class Point:
    __slots__ = ('x', 'y',)

    def __init__(self, x, y):
        self.x = x
        self.y = y

# При таком классическом определении класса Point создать новую точку можно семью способами

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

На примере point6 мы видим, чтов  Python уже встроена поддержка прототипов в виде функции copy.deepcopy(). Однако пример point7 показывает, что в Python есть средства и поулчше: вместо того чтобы клонировать существующий объект и модифицировать клон, Python предоставляет доступ к объекту класса имеющегося объекта и таким образом мы можем создать новый объект непосредственно, что гораздо эффективнее клонирования.

Прототип - паттерн, порождающий объекты. Задает виды создаваемых объектов с помощью экземпляра-прототипа и создает новые объекты путем копирования этого прототипа.

```python
"""
*What is this pattern about?
This patterns aims to reduce the number of classes required by an
application. Instead of relying on subclasses it creates objects by
copying a prototypical instance at run-time.
This is useful as it makes it easier to derive new kinds of objects,
when instances of the class have only a few different combinations of
state, and when instantiation is expensive.
*What does this example do?
When the number of prototypes in an application can vary, it can be
useful to keep a Dispatcher (aka, Registry or Manager). This allows
clients to query the Dispatcher for a prototype before cloning a new
instance.
Below provides an example of such Dispatcher, which contains three
copies of the prototype: 'default', 'objecta' and 'objectb'.
*TL;DR
Creates new object instances by cloning prototype.
"""


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

#### Одиночка (Singleton)

Паттерн Одиночка (Синглтон) применяется, когда необходим класс, у которого должен быть единственный экземпляр во всей программе.

С помощью паттерна одиночка могут быть реализованы многие паттерны (абстрактная фабрика, строитель, прототип).

В сборнике рецептов приводится простой класс Singleton, которому любой класс может унаследовать, чтобы стать одиночкой.

```python
"""
Yet one singleton realization on Python without metaclass. Singleton may has __init__ method which will call only when first object create.
http://code.activestate.com/recipes/577208-singletonsubclass-with-once-initialization/
"""


class Singleton(object):

    def __new__(cls,*dt,**mp):
        if not hasattr(cls,'_inst'):
            cls._inst = super(Singleton, cls).__new__(cls,dt,mp)
        else:
            def init_pass(self,*dt,**mp):pass
            cls.__init__ = init_pass

        return cls._inst

if __name__ == '__main__':


    class A(Singleton):

        def __init__(self):
            """Super constructor
                There is we can open file or create connection to the database
            """
            print "A init"


    a1 = A()
    a2 = A()
```

И класс Borg, который даст тот же результат совсем другим способом.

```python
"""
*What is this pattern about?
The Borg pattern (also known as the Monostate pattern) is a way to
implement singleton behavior, but instead of having only one instance
of a class, there are multiple instances that share the same state. In
other words, the focus is on sharing state instead of sharing instance
identity.
*What does this example do?
To understand the implementation of this pattern in Python, it is
important to know that, in Python, instance attributes are stored in a
attribute dictionary called __dict__. Usually, each instance will have
its own dictionary, but the Borg pattern modifies this so that all
instances have the same dictionary.
In this example, the __shared_state attribute will be the dictionary
shared between all instances, and this is ensured by assigining
__shared_state to the __dict__ variable when initializing a new
instance (i.e., in the __init__ method). Other attributes are usually
added to the instance's attribute dictionary, but, since the attribute
dictionary itself is shared (which is __shared_state), all other
attributes will also be shared.
*Where is the pattern used practically?
Sharing state is useful in applications like managing database connections:
https://github.com/onetwopunch/pythonDbTemplate/blob/master/database.py
*References:
https://fkromer.github.io/python-pattern-references/design/#singleton
*TL;DR
Provides singleton-like behavior sharing state between instances.
"""


class Borg:
    __shared_state = {}

    def __init__(self):
        self.__dict__ = self.__shared_state
        self.state = 'Init'

    def __str__(self):
        return self.state


class YourBorg(Borg):
    pass


def main():
    """
    >>> rm1 = Borg()
    >>> rm2 = Borg()
    >>> rm1.state = 'Idle'
    >>> rm2.state = 'Running'
    >>> print('rm1: {0}'.format(rm1))
    rm1: Running
    >>> print('rm2: {0}'.format(rm2))
    rm2: Running
    # When the `state` attribute is modified from instance `rm2`,
    # the value of `state` in instance `rm1` also changes
    >>> rm2.state = 'Zombie'
    >>> print('rm1: {0}'.format(rm1))
    rm1: Zombie
    >>> print('rm2: {0}'.format(rm2))
    rm2: Zombie
    # Even though `rm1` and `rm2` share attributes, the instances are not the same
    >>> rm1 is rm2
    False
    # Shared state is also modified from a subclass instance `rm3`
    >>> rm3 = YourBorg()
    >>> print('rm1: {0}'.format(rm1))
    rm1: Init
    >>> print('rm2: {0}'.format(rm2))
    rm2: Init
    >>> print('rm3: {0}'.format(rm3))
    rm3: Init
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

Однако самый простой способ получить функциональность одиночки в Python - создать модуль с глобальным состоянием, которое хранится в закрытых переменных, и предоставить открытые функции для доступа к нему. Например, для получения курсов валют нам понадобится функция, которая будет возвращать словарь (ключ - название валюты, значение - обменный курс). Возможно, эту функцию понадобится вызывать несколько раз, но в большинстве случев извлекать откуда-то курсы нужно единожды. Реализовать это поможет паттерн Одиночка.

```python
#!/usr/bin/env python3
# Copyright © 2012-13 Qtrac Ltd. All rights reserved.
# This program or module is free software: you can redistribute it
# and/or modify it under the terms of the GNU General Public License as
# published by the Free Software Foundation, either version 3 of the
# License, or (at your option) any later version. It is provided for
# educational purposes and is distributed in the hope that it will be
# useful, but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
# General Public License for more details.

import re
import urllib.request


_URL = "http://www.bankofcanada.ca/stats/assets/csv/fx-seven-day.csv"


def get(refresh=False):
    if refresh:
        get.rates = {}
    if get.rates:
        return get.rates
    with urllib.request.urlopen(_URL) as file:
        for line in file:
            line = line.rstrip().decode("utf-8")
            if not line or line.startswith(("#", "Date")):
                continue
            name, currency, *rest = re.split(r"/s*,/s*", line)
            key = "{} ({})".format(name, currency)
            try:
                get.rates[key] = float(rest[-1])
            except ValueError as err:
                print("error {}: {}".format(err, line))
    return get.rates
get.rates = {}


if __name__ == "__main__":
    import sys
    if sys.stdout.isatty():
        print(get())
    else:
        print("Loaded OK")

```

Здесь мы создаем словарь rates в виде атрибута функции Rates.get() - это наше закрытое значение. Когда открытая функция get() вызывается в первый раз (а также при вызове с параметром refresh=True), мы загружаем список курсов; в противном случае просто возвращаем последние загруженные курсы.

#### Порождающие паттерны. Итог

Все порождающие паттерны проектирования реализуются на Python тривиально. Паттерн Одиночка можно реализовать непосредственно с помощью модуля, а паттерн Прототип вообще ни к чему (хотя его можно реализовать с помощью модуля copy), так как Python дает динамический доступ к объектам классов. Из порождающих паттернов наиболее полезны Фабрика и Построитель, и реализовать их можно несколькими способами.

### Структурные (Structural)

Структурные паттерны описывают, как из одних объектов составляются другие, более крупные. Рассматриваются три основных круга вопросов: адаптация интерфейсов, добавление функциональности и работа с коллекциями объектов.

#### Адаптер (Adapter)

Паттерн Адаптер описывает технику адаптации интерфейса. Задача состоит в том, чтобы один класс мог воспользоваться другим - с несовместимым интерфейсом - без внесения каких-либо изменений в оба класса. Это полезно, например, когда требуется воспользоваться не подлежащим изменению классом в контексте, на который он не был расчитан.

Адаптер обеспечивает совместную работу классов с несовместимыми интерфейсами, которая без него была бы невозможна.

```python
"""
*What is this pattern about?
The Adapter pattern provides a different interface for a class. We can
think about it as a cable adapter that allows you to charge a phone
somewhere that has outlets in a different shape. Following this idea,
the Adapter pattern is useful to integrate classes that couldn't be
integrated due to their incompatible interfaces.
*What does this example do?
The example has classes that represent entities (Dog, Cat, Human, Car)
that make different noises. The Adapter class provides a different
interface to the original methods that make such noises. So the
original interfaces (e.g., bark and meow) are available under a
different name: make_noise.
*Where is the pattern used practically?
The Grok framework uses adapters to make objects work with a
particular API without modifying the objects themselves:
http://grok.zope.org/doc/current/grok_overview.html#adapters
*References:
http://ginstrom.com/scribbles/2008/11/06/generic-adapter-class-in-python/
https://sourcemaking.com/design_patterns/adapter
http://python-3-patterns-idioms-test.readthedocs.io/en/latest/ChangeInterface.html#adapter
*TL;DR
Allows the interface of an existing class to be used as another interface.
"""


class Dog:
    def __init__(self):
        self.name = "Dog"

    def bark(self):
        return "woof!"


class Cat:
    def __init__(self):
        self.name = "Cat"

    def meow(self):
        return "meow!"


class Human:
    def __init__(self):
        self.name = "Human"

    def speak(self):
        return "'hello'"


class Car:
    def __init__(self):
        self.name = "Car"

    def make_noise(self, octane_level):
        return "vroom{0}".format("!" * octane_level)


class Adapter:
    """
    Adapts an object by replacing methods.
    Usage:
    dog = Dog()
    dog = Adapter(dog, make_noise=dog.bark)
    """

    def __init__(self, obj, **adapted_methods):
        """We set the adapted methods in the object's dict"""
        self.obj = obj
        self.__dict__.update(adapted_methods)

    def __getattr__(self, attr):
        """All non-adapted calls are passed to the object"""
        return getattr(self.obj, attr)

    def original_dict(self):
        """Print original object dict"""
        return self.obj.__dict__


def main():
    """
    >>> objects = []
    >>> dog = Dog()
    >>> print(dog.__dict__)
    {'name': 'Dog'}
    >>> objects.append(Adapter(dog, make_noise=dog.bark))
    >>> objects[0].__dict__['obj'], objects[0].__dict__['make_noise']
    (<...Dog object at 0x...>, <bound method Dog.bark of <...Dog object at 0x...>>)
    >>> print(objects[0].original_dict())
    {'name': 'Dog'}
    >>> cat = Cat()
    >>> objects.append(Adapter(cat, make_noise=cat.meow))
    >>> human = Human()
    >>> objects.append(Adapter(human, make_noise=human.speak))
    >>> car = Car()
    >>> objects.append(Adapter(car, make_noise=lambda: car.make_noise(3)))
    >>> for obj in objects:
    ...    print("A {0} goes {1}".format(obj.name, obj.make_noise()))
    A Dog goes woof!
    A Cat goes meow!
    A Human goes 'hello'
    A Car goes vroom!!!
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

#### Мост (Bridge)

Мост (Bridge) - паттерн, структурирующий объекты. Основная задача - отделить абстракцию от её реализации так, чтобы то и другое можно было изменять независимо.

Традиционный подход без использования паттерна Мост состоит в том, чтобы создать один или несколько абстрактных базовых классов, а затем предоставить две или более конкретных реализации каждого базового класса.
А паттерн Мост предлагает создать две независимых иерархии классов: "абстрактную", которая определяет операции (например интерфейс или алгоритм верхнего уровня) и конкретную, предоставляющую реализацию, которые в конечном итоге и будут вызваны из абстрактных операций. "Абстрактный" класс агрегирует экземпляр одного из конкретных классов с реализацией - и этот последний служит *мостом* между абстрактным интерфейсом и конкретными операциями.

```python
"""
*References:
http://en.wikibooks.org/wiki/Computer_Science_Design_Patterns/Bridge_Pattern#Python
*TL;DR
Decouples an abstraction from its implementation.
"""


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

#### Компоновщик (Composite)

Паттерн Компоновщик позволяет единообразно обрабатывать объекты, образующие иерархию, вне зависимости от того, содержат они другие объекты или нет. Такие объекты называют составными.

В классическом решении составные объекты - как отдельные, так и коллекции - имеют один и тот же базовый класс. У составных и несоставных объектов обычно одни и те же основные методы, но составные объекты добавляют методы для поддержки добавления, удаления и перебора дочерних объектов.

Этот паттерн часто применяется в программах рисования, например Inkscape, для поддержки группировки и разгруппировки. Его полезность в таких ситуациях объясняется тем, что подлежащие группировке или разгруппировке компоненты могут быть как одиночными (например прямоугольник) так и состаными (например, рожица, составленная из нескольких разных фигур)

```python
"""
*What is this pattern about?
The composite pattern describes a group of objects that is treated the
same way as a single instance of the same type of object. The intent of
a composite is to "compose" objects into tree structures to represent
part-whole hierarchies. Implementing the composite pattern lets clients
treat individual objects and compositions uniformly.
*What does this example do?
The example implements a graphic class，which can be either an ellipse
or a composition of several graphics. Every graphic can be printed.
*Where is the pattern used practically?
In graphics editors a shape can be basic or complex. An example of a
simple shape is a line, where a complex shape is a rectangle which is
made of four line objects. Since shapes have many operations in common
such as rendering the shape to screen, and since shapes follow a
part-whole hierarchy, composite pattern can be used to enable the
program to deal with all shapes uniformly.
*References:
https://en.wikipedia.org/wiki/Composite_pattern
https://infinitescript.com/2014/10/the-23-gang-of-three-design-patterns/
*TL;DR
Describes a group of objects that is treated as a single instance.
"""


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

#### Декоратор (Decorator)

Декоратором называется функция, которая принимает функцию с таким же именем, как у исходной, но с расширенной функциональностью. Декораторы часто используются во фреймвоках, чтобы упростить интеграцию пользовательских функций с фреймворком.

Паттерн Декоратор настолько полезен, что в Python встроена специальная поддержка для него. В Python декорировать можно как функции, так и методы. Кроме того, Python поддерживает декораторы классов: функции, которые принимают клас в качестве аргумента и возвращают новый класс с таким же именем, как у исходного, но дополненной функциональностью.

Иногда декораторы классов удобно использовать как альтернативу производным классам.

```python
"""
*What is this pattern about?
The Decorator pattern is used to dynamically add a new feature to an
object without changing its implementation. It differs from
inheritance because the new feature is added only to that particular
object, not to the entire subclass.
*What does this example do?
This example shows a way to add formatting options (boldface and
italic) to a text by appending the corresponding tags (<b> and
<i>). Also, we can see that decorators can be applied one after the other,
since the original text is passed to the bold wrapper, which in turn
is passed to the italic wrapper.
*Where is the pattern used practically?
The Grok framework uses decorators to add functionalities to methods,
like permissions or subscription to an event:
http://grok.zope.org/doc/current/reference/decorators.html
*References:
https://sourcemaking.com/design_patterns/decorator
*TL;DR
Adds behaviour to object without affecting its class.
"""


class TextTag:
    """Represents a base text tag"""

    def __init__(self, text):
        self._text = text

    def render(self):
        return self._text


class BoldWrapper(TextTag):
    """Wraps a tag in <b>"""

    def __init__(self, wrapped):
        self._wrapped = wrapped

    def render(self):
        return "<b>{}</b>".format(self._wrapped.render())


class ItalicWrapper(TextTag):
    """Wraps a tag in <i>"""

    def __init__(self, wrapped):
        self._wrapped = wrapped

    def render(self):
        return "<i>{}</i>".format(self._wrapped.render())


if __name__ == '__main__':
    simple_hello = TextTag("hello, world!")
    special_hello = ItalicWrapper(BoldWrapper(simple_hello))
    print("before:", simple_hello.render())
    print("after:", special_hello.render())

# OUTPUT #
# before: hello, world!
# after: <i><b>hello, world!</b></i>
```

#### Фасад (Facade)

Паттерн Фасад служит для того, чтобы предоставить упрощенный унифицированный интерфейс к подсистеме, чей истинный интерфейс слишком сложен или написан на таком низком уровне, что работать с ним неудобно. Фасад определяет интерфейс более высокого уровня, который упрощает использование подсистемы.

В стандартной библиотеке Python имеется несколько модулей для работы с сжатыми файлами - gzip, tar+gzip, zip. Все они имеют разные интерфейсы. Если мы хотим иметь один унифицированный интерфейс для работы с архивами, мы можем воспользоваться паттерном Фасад.

Паттерны Фасад и Адаптер на первый взгляд кажутся похожими. Разница в том, что Фасад надстраивает простой интерфейс поверх сложного, а Адаптер надстраивает унифицированный интерфейс над каким-то другим (необязательно сложным). Оба эти паттерна можно использовать совместно. Например определить интерфейс для работы с архивными файлами, написать адапрет для каждого формата и надстроить поверх них фасад, чтобы пользователям не нужно было беспокоиться о том, какой конкретно формат файла используется.

```python
"""
Example from https://en.wikipedia.org/wiki/Facade_pattern#Python
*What is this pattern about?
The Facade pattern is a way to provide a simpler unified interface to
a more complex system. It provides an easier way to access functions
of the underlying system by providing a single entry point.
This kind of abstraction is seen in many real life situations. For
example, we can turn on a computer by just pressing a button, but in
fact there are many procedures and operations done when that happens
(e.g., loading programs from disk to memory). In this case, the button
serves as an unified interface to all the underlying procedures to
turn on a computer.
*Where is the pattern used practically?
This pattern can be seen in the Python standard library when we use
the isdir function. Although a user simply uses this function to know
whether a path refers to a directory, the system makes a few
operations and calls other modules (e.g., os.stat) to give the result.
*References:
https://sourcemaking.com/design_patterns/facade
https://fkromer.github.io/python-pattern-references/design/#facade
http://python-3-patterns-idioms-test.readthedocs.io/en/latest/ChangeInterface.html#facade
*TL;DR
Provides a simpler unified interface to a complex system.
"""


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

#### Приспособленец (Flyweight)

Приспособленец предназначен для обработки большого числа сравнительно небольших объектов, когда многие из этих объектов являются дубликатами. Реализация паттерна предполагает, что каждый уникальный объект представлется всего один раз и именно этот экземпляр отдается на запрос. В Python легко реализуется через словарь.

В Python подход к реализации приспособленцев естественный - благодаря наличию ссылок на объекты. Например, если бы у нас был длинный список строк, в котором много дубликатов, то, сохраняя ссылки на объекты (то есть переменные), а не литеральные строки, мы бы могли существенно сэкономить память

```python
red, green, blue = 'red', 'green', 'blue'
x = (red, green, blue, red, green, blue, green)
```

```python
"""
*What is this pattern about?
This pattern aims to minimise the number of objects that are needed by
a program at run-time. A Flyweight is an object shared by multiple
contexts, and is indistinguishable from an object that is not shared.
The state of a Flyweight should not be affected by it's context, this
is known as its intrinsic state. The decoupling of the objects state
from the object's context, allows the Flyweight to be shared.
*What does this example do?
The example below sets-up an 'object pool' which stores initialised
objects. When a 'Card' is created it first checks to see if it already
exists instead of creating a new one. This aims to reduce the number of
objects initialised by the program.
*References:
http://codesnipers.com/?q=python-flyweights
https://python-patterns.guide/gang-of-four/flyweight/
*Examples in Python ecosystem:
https://docs.python.org/3/library/sys.html#sys.intern
*TL;DR
Minimizes memory usage by sharing data with other similar objects.
"""

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

#### Заместитель (Proxy)

Паттерн Заместитель применяется когда мы хотим подставить один объект вместо другого. В книге "Паттенрны проектирования" описаны 4 таких случая:

1. удаленный прокси, когда доступ к удаленному объекту проксируется локальным объектом;
2. вирутальный прокси, который позволяет создавать облегченные объекты вместо тяжеловесных, а последние создавать только когда это необходимо;
3. защитный прокси, который предоставляет различные уровни доступа, в зависимости от прав клиента;
4. интелектуальная сслыка, которая выполняет "дополнительные действия при обращении к объекту" (можно также реализовать с помощью дескриптопа @property)

Mock - пример реализации паттерна Заместитель

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

#### Структурные паттерны. Итог

Паттерны Адаптер и Фасад упрощают повторное использование классов в новых контекстах, а паттерн Мост дает возможность внедрить сложную функциональность одного класса в другой. Компоновщик упрощает создание иерархий объектов, хотя в Python это не особенно нужно, так как для этой цели хватает словарей. Декоратор настолько полезен, что в Python для него имеется прямая поддержка, причем идея декоратора распространена даже на классы. Использование ссылок на объекты означает что в сам язык встроена варианция на тему паттерна Приспособленец. А паттерн Заместитель в Python реализовать особенно просто.

### Поведенческие (Behavioral)

Предмет поведенческих паттерном - способ решения задачи, то есть они имеют дело с алгоритмами и взаимодействиями объектов. Эти паттерны предлагают действенные способы обдумывания и организации вычислений. Для некоторых из них имеется прямяая поддержка в синтаксисе Python.

#### Цепочка ответственности (Chain of responsobility)

Паттерн цепочка отвестственности предназначен, для того чтобы разорвать связь между отправителем запроса и получателем, который этот запрос обрабатывает. Вместо непосредственного вызова одной функции из другой первая функция отправляет запрос цепочке получателей. Первый получатель в цепочке может либо обработать запрос и прервать цепочку (не передавая запрос дальше), либо передать запрос следующему получателю. У второго получателя есть такой же выбор и так далее, пока запрос не дойдет до последнего получателя (который может отбросить запрос или возбудить исключение).

Представьте себе пользовательский интерфейс, который получает события для обработки. Одни события поступают от пользователя (например, события мыши и клавиатуры), другие - от системы (например, события таймера).

```python
"""
*What is this pattern about?
The Chain of responsibility is an object oriented version of the
`if ... elif ... elif ... else ...` idiom, with the
benefit that the condition–action blocks can be dynamically rearranged
and reconfigured at runtime.
This pattern aims to decouple the senders of a request from its
receivers by allowing request to move through chained
receivers until it is handled.
Request receiver in simple form keeps a reference to a single successor.
As a variation some receivers may be capable of sending requests out
in several directions, forming a `tree of responsibility`.
*TL;DR
Allow a request to pass down a chain of receivers until it is handled.
"""

import abc


class Handler(metaclass=abc.ABCMeta):

    def __init__(self, successor=None):
        self.successor = successor

    def handle(self, request):
        """
        Handle request and stop.
        If can't - call next handler in chain.
        As an alternative you might even in case of success
        call the next handler.
        """
        res = self.check_range(request)
        if not res and self.successor:
            self.successor.handle(request)

    @abc.abstractmethod
    def check_range(self, request):
        """Compare passed value to predefined interval"""


class ConcreteHandler0(Handler):
    """Each handler can be different.
    Be simple and static...
    """

    @staticmethod
    def check_range(request):
        if 0 <= request < 10:
            print("request {} handled in handler 0".format(request))
            return True


class ConcreteHandler1(Handler):
    """... With it's own internal state"""

    start, end = 10, 20

    def check_range(self, request):
        if self.start <= request < self.end:
            print("request {} handled in handler 1".format(request))
            return True


class ConcreteHandler2(Handler):
    """... With helper methods."""

    def check_range(self, request):
        start, end = self.get_interval_from_db()
        if start <= request < end:
            print("request {} handled in handler 2".format(request))
            return True

    @staticmethod
    def get_interval_from_db():
        return (20, 30)


class FallbackHandler(Handler):
    @staticmethod
    def check_range(request):
        print("end of chain, no handler for {}".format(request))
        return False


def main():
    """
    >>> h0 = ConcreteHandler0()
    >>> h1 = ConcreteHandler1()
    >>> h2 = ConcreteHandler2(FallbackHandler())
    >>> h0.successor = h1
    >>> h1.successor = h2
    >>> requests = [2, 5, 14, 22, 18, 3, 35, 27, 20]
    >>> for request in requests:
    ...     h0.handle(request)
    request 2 handled in handler 0
    request 5 handled in handler 0
    request 14 handled in handler 1
    request 22 handled in handler 2
    request 18 handled in handler 1
    request 3 handled in handler 0
    end of chain, no handler for 35
    request 27 handled in handler 2
    request 20 handled in handler 2
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

#### Команда (Command)

паттерн Команда применяется для инкапсуляции команд в виде объектов. Например, с его помощью можно построить последовательность команд для отложенного выполнения или создать команды, допускающие отмену.

```python
"""
*TL;DR
Encapsulates all information needed to perform an action or trigger an event.
*Examples in Python ecosystem:
Django HttpRequest (without `execute` method):
 https://docs.djangoproject.com/en/2.1/ref/request-response/#httprequest-objects
"""

import os


class MoveFileCommand:
    def __init__(self, src, dest):
        self.src = src
        self.dest = dest

    def execute(self):
        self.rename(self.src, self.dest)

    def undo(self):
        self.rename(self.dest, self.src)

    def rename(self, src, dest):
        print("renaming {} to {}".format(src, dest))
        os.rename(src, dest)


def main():
    """
    >>> from os.path import lexists
    >>> command_stack = [
    ...     MoveFileCommand('foo.txt', 'bar.txt'),
    ...     MoveFileCommand('bar.txt', 'baz.txt')
    ... ]
    # Verify that none of the target files exist
    >>> assert not lexists("foo.txt")
    >>> assert not lexists("bar.txt")
    >>> assert not lexists("baz.txt")
    # Create empty file
    >>> open("foo.txt", "w").close()
    # Commands can be executed later on
    >>> for cmd in command_stack:
    ...     cmd.execute()
    renaming foo.txt to bar.txt
    renaming bar.txt to baz.txt
    # And can also be undone at will
    >>> for cmd in reversed(command_stack):
    ...     cmd.undo()
    renaming baz.txt to bar.txt
    renaming bar.txt to foo.txt
    >>> os.unlink("foo.txt")
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

#### Интерпретатор (Interpreter)

Паттерн Интерпретатор формализует два типичных требования: предоставить средства, с помощью которых пользователь мог бы вводить в программу нестроковые значения, и дать пользователям возможность создавать программы.

На самом примитивном уровне  приложение получает от пользователя, или от другой программы, строки, которые необходимо каким-то образом интерпретировать (и, быть может, выполнить).

Примером широко распространенного воплощения таких требований является создание предметно-ориентированных языков (DSL).

```python
"""
Интерпретатор (Interpreter) - паттерн поведения классов.
Для заданного языка определяет представление его грамматики,
а также интерпретатор предложений этого языка.
"""


class RomanNumeralInterpreter(object):
    """Интерпретатор римских цифр"""
    def __init__(self):
        self.grammar = {
            'I': 1,
            'V': 5,
            'X': 10,
            'L': 50,
            'C': 100,
            'D': 500,
            'M': 1000
        }

    def interpret(self, text):
        numbers = map(self.grammar.get, text)  # строки в значения
        if None in numbers:
            raise ValueError('Ошибочное значение: %s' % text)
        result = 0  # накапливаем результат
        temp = None  # запоминаем последнее значение
        while numbers:
            num = numbers.pop(0)
            if temp is None or temp >= num:
                result += num
            else:
                result += (num - temp * 2)
            temp = num
        return result


interp = RomanNumeralInterpreter()
print interp.interpret('MMMCMXCIX') == 3999  # True
print interp.interpret('MCMLXXXVIII') == 1988  # True
```

#### Итератор (Iterator)

паттерн Итератор позвояет последовательно обойти элементы коллекции или агрегированного объекта, не раскрывая деталей их внутреннего устройства. Он настолько полезен, что в Python встроена его поддержка, а кроме того, предоставляются специальные методы, которые мы можем реализовать в собственных классах, чтобы органично поддержать итерирование.

Итерирование можно поддержать тремя способами: следуя протоколу последовательности, пользуясь вариантом встроенной функции iter() с двумя агрументами или следуя протоколу итератора.

```python
#!/usr/bin/env python3
# Copyright © 2012-13 Qtrac Ltd. All rights reserved.
# This program or module is free software: you can redistribute it and/or
# modify it under the terms of the GNU General Public License as published
# by the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version. It is provided for educational
# purposes and is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
# General Public License for more details.


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

#### Посредник (Mediator)

Паттерн Посредник представляет средства для создания объекта - посредника - который инкапсулирует взаимодействия между другими объектами. Это позволяет осуществлять взаимодействия между объектами, которые ничего не знают друг о друге. Например, в случае нажатия кнопки соответствующий ей объект должен только известить посредника, а уж тот уведомит все объекты, которых интересует нажатие этой кнопки.

Посредник обеспечивает слабую связанность системы, избавляя объекты от необъодимости явно ссылаться друг на друга и позволяя тем самым независимо изменять взаимодействия между ними.

```python
"""
https://www.djangospin.com/design-patterns-python/mediator/
Objects in a system communicate through a Mediator instead of directly with each other.
This reduces the dependencies between communicating objects, thereby reducing coupling.
*TL;DR
Encapsulates how a set of objects interact.
"""


class ChatRoom:
    """Mediator class"""

    def display_message(self, user, message):
        print("[{} says]: {}".format(user, message))


class User:
    """A class whose instances want to interact with each other"""

    def __init__(self, name):
        self.name = name
        self.chat_room = ChatRoom()

    def say(self, message):
        self.chat_room.display_message(self, message)

    def __str__(self):
        return self.name


def main():
    """
    >>> molly = User('Molly')
    >>> mark = User('Mark')
    >>> ethan = User('Ethan')
    >>> molly.say("Hi Team! Meeting at 3 PM today.")
    [Molly says]: Hi Team! Meeting at 3 PM today.
    >>> mark.say("Roger that!")
    [Mark says]: Roger that!
    >>> ethan.say("Alright.")
    [Ethan says]: Alright.
    """


if __name__ == '__main__':
    import doctest
    doctest.testmod()
```

Еще пример

```python
#!/usr/bin/env python3
# Copyright © 2012-13 Qtrac Ltd. All rights reserved.
# This program or module is free software: you can redistribute it
# and/or modify it under the terms of the GNU General Public License as
# published by the Free Software Foundation, either version 3 of the
# License, or (at your option) any later version. It is provided for
# educational purposes and is distributed in the hope that it will be
# useful, but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
# General Public License for more details.

import collections


def main():
    form = Form()
    test_user_interaction_with(form)


class Form:

    def __init__(self):
        self.create_widgets()
        self.create_mediator()


    def create_widgets(self):
        self.nameText = Text()
        self.emailText = Text()
        self.okButton = Button("OK")
        self.cancelButton = Button("Cancel")


    def create_mediator(self):
        self.mediator = Mediator(((self.nameText, self.update_ui),
                (self.emailText, self.update_ui),
                (self.okButton, self.clicked),
                (self.cancelButton, self.clicked)))
        self.update_ui()


    def update_ui(self, widget=None):
        self.okButton.enabled = (bool(self.nameText.text) and
                                 bool(self.emailText.text))


    def clicked(self, widget):
        if widget == self.okButton:
            print("OK")
        elif widget == self.cancelButton:
            print("Cancel")


class Mediator:

    def __init__(self, widgetCallablePairs):
        self.callablesForWidget = collections.defaultdict(list)
        for widget, caller in widgetCallablePairs:
            self.callablesForWidget[widget].append(caller)
            widget.mediator = self


    def on_change(self, widget):
        callables = self.callablesForWidget.get(widget)
        if callables is not None:
            for caller in callables:
                caller(widget)
        else:
            raise AttributeError("No on_change() method registered for {}"
                    .format(widget))


class Mediated:

    def __init__(self):
        self.mediator = None


    def on_change(self):
        if self.mediator is not None:
            self.mediator.on_change(self)


class Button(Mediated):

    def __init__(self, text=""):
        super().__init__()
        self.enabled = True
        self.text = text


    def click(self):
        if self.enabled:
            self.on_change()


    def __str__(self):
        return "Button({!r}) {}".format(self.text,
                "enabled" if self.enabled else "disabled")


class Text(Mediated):

    def __init__(self, text=""):
        super().__init__()
        self.__text = text


    @property
    def text(self):
        return self.__text


    @text.setter
    def text(self, text):
        if self.text != text:
            self.__text = text
            self.on_change()


    def __str__(self):
        return "Text({!r})".format(self.text)


def test_user_interaction_with(form):
    form.okButton.click()           # Ignored because it is disabled
    print(form.okButton.enabled)    # False
    form.nameText.text = "Fred"
    print(form.okButton.enabled)    # False
    form.emailText.text = "fred@bloggers.com"
    print(form.okButton.enabled)    # True
    form.okButton.click()           # OK
    form.emailText.text = ""
    print(form.okButton.enabled)    # False
    form.cancelButton.click()       # Cancel


if __name__ == "__main__":
    main()

```

#### Хранитель (Memento)

Паттерн хранитель служит для сохранения и восстановленя состояния объекта, не нарушая инкапсуляцию.

В языке Python имеется готовая поддержка этого паттерна; с помощью модуля `pickle` мы можем сериализовать и десериализовать произвольные объекты Python (с некоторыми ограничениями, например, нельзя сериализовать файловый объект).

Даже в тех редких случаях, когда мы сталкиваемся с ограничением сериализации, всегда можно добавить собственную поддержку этого механизам, например, реализовав специальные методы `__getstate__()` и `__setstate__()` и, возможно, метод `__getnewargs__()`. Аналогично если мы захотим использовать формат JSON для своих классов, то сможем расширить кодировщик и декодировщик ищ модуля `json`.

Можно было бы придумать собственный формат и протоколы, но смысла в это немного, так как Python и так предоставляет развитую поддержку этого паттерна.

```python
"""
http://code.activestate.com/recipes/413838-memento-closure/
*TL;DR
Provides the ability to restore an object to its previous state.
"""

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

#### Наблюдатель (Observer)

Паттерн Наблюдатель поддерживает отношения зависимости многие-ко-многим между объектами, например, когда изменяется состояние одного объекта, уведомляются все связанные с ним объекты. В наши дни, наверное самый распростарненный пример этого паттерна и его вариантов - парадигма модель-представление-контроллер (MVC). В этой парадигме модель описывает данные, одно или несколько предствалений эти данные визиалируют, а одни или несколько контроллеров осуществляют посредничество между вводом (например, взаимодействие с пользователем) и моделью. И любые изменения в модели автоматически отражаются в ассоциированных с ней представлениях.

У подхода MVC есть одно популярное упрощение - использовать только модели и представления, но поручить представлениям как визуализацию данных, так и передачу модели входных данных; иными словами, представления совмещены с контроллерами. В терминах паттерна Наблюдатель это означает, что представления - наблюдатели, а модель - наблюдаемый объект.

В качестве примеров можно назвать триггеры в базах данных, систему сигнализации Django, механизм сигналов и слотов в библиотеке QT и многочисленные применения технологии WebSockets.

```python
"""
http://code.activestate.com/recipes/131499-observer-pattern/
*TL;DR
Maintains a list of dependents and notifies them of any state changes.
*Examples in Python ecosystem:
Django Signals: https://docs.djangoproject.com/en/2.1/topics/signals/
Flask Signals: http://flask.pocoo.org/docs/1.0/signals/
"""


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

#### Состояние (State)

Паттерн Состояние предназначен для создания объектов, поведение которых изменяется при изменении состояния; это означает, что у объекта есть режими работы. Извне создается впечатление, что изменился класс объекта.

К обработке состояния, хранящегося внутри класса, есть два основных подхода. Первый - использование методов, чувствительных к состоянию. Второй - использование определяемых состоянием методов.

```python
"""
Implementation of the state pattern
http://ginstrom.com/scribbles/2007/10/08/design-patterns-python-style/
*TL;DR
Implements state as a derived class of the state pattern interface.
Implements state transitions by invoking methods from the pattern's superclass.
"""


class State:

    """Base state. This is to share functionality"""

    def scan(self):
        """Scan the dial to the next station"""
        self.pos += 1
        if self.pos == len(self.stations):
            self.pos = 0
        print("Scanning... Station is {} {}".format(self.stations[self.pos], self.name))


class AmState(State):
    def __init__(self, radio):
        self.radio = radio
        self.stations = ["1250", "1380", "1510"]
        self.pos = 0
        self.name = "AM"

    def toggle_amfm(self):
        print("Switching to FM")
        self.radio.state = self.radio.fmstate


class FmState(State):
    def __init__(self, radio):
        self.radio = radio
        self.stations = ["81.3", "89.1", "103.9"]
        self.pos = 0
        self.name = "FM"

    def toggle_amfm(self):
        print("Switching to AM")
        self.radio.state = self.radio.amstate


class Radio:

    """A radio. It has a scan button, and an AM/FM toggle switch."""

    def __init__(self):
        """We have an AM state and an FM state"""
        self.amstate = AmState(self)
        self.fmstate = FmState(self)
        self.state = self.amstate

    def toggle_amfm(self):
        self.state.toggle_amfm()

    def scan(self):
        self.state.scan()


def main():
    """
    >>> radio = Radio()
    >>> actions = [radio.scan] * 2 + [radio.toggle_amfm] + [radio.scan] * 2
    >>> actions *= 2
    >>> for action in actions:
    ...    action()
    Scanning... Station is 1380 AM
    Scanning... Station is 1510 AM
    Switching to FM
    Scanning... Station is 89.1 FM
    Scanning... Station is 103.9 FM
    Scanning... Station is 81.3 FM
    Scanning... Station is 89.1 FM
    Switching to AM
    Scanning... Station is 1250 AM
    Scanning... Station is 1380 AM
    """


if __name__ == '__main__':
    import doctest
    doctest.testmod()
```

Еще пример

```python
"""
Состояние (State) - паттерн поведения объектов.
Позволяет объекту варьировать свое поведение в зависимости от внутреннего состояния.
Извне создается впечатление, что изменился класс объекта.
"""


class LampStateBase(object):
    """Состояние лампы"""
    def get_color(self):
        raise NotImplementedError()


class GreenLampState(LampStateBase):
    def get_color(self):
        return 'Green'


class RedLampState(LampStateBase):
    def get_color(self):
        return 'Red'


class BlueLampState(LampStateBase):
    def get_color(self):
        return 'Blue'


class Lamp(object):
    def __init__(self):
        self._current_state = None
        self._states = self.get_states()

    def get_states(self):
        return [GreenLampState(), RedLampState(), BlueLampState()]

    def next_state(self):
        if self._current_state is None:
            self._current_state = self._states[0]
        else:
            index = self._states.index(self._current_state)
            if index < len(self._states) - 1:
                index += 1
            else:
                index = 0
            self._current_state = self._states[index]
        return self._current_state

    def light(self):
        state = self.next_state()
        print state.get_color()


lamp = Lamp()
[lamp.light() for i in range(3)]
# Green
# Red
# Blue
[lamp.light() for i in range(3)]
# Green
# Red
# Blue
```

#### Стратегия (Strategy)

Паттерн Стратегия позволяет инкапсулировать набор взаимозаменяемых алгоритмов, из которых пользователь выбирает тот, что ему нужен.

```python
"""
Стратегия (Strategy) - паттерн поведения объектов.
Определяет семейство алгоритмов, инкапсулирует каждый из них и делает их взаимозаменяемыми.
Стратегия позволяет изменять алгоритмы независимо от клиентов, которые ими пользуются.
"""


class ImageDecoder(object):
    @staticmethod
    def decode(filename):
        raise NotImplementedError()


class PNGImageDecoder(ImageDecoder):
    @staticmethod
    def decode(filename):
        print 'PNG decode'


class JPEGImageDecoder(ImageDecoder):
    @staticmethod
    def decode(filename):
        print 'JPEG decode'


class GIFImageDecoder(ImageDecoder):
    @staticmethod
    def decode(filename):
        print 'GIF decode'


class Image(object):
    @classmethod
    def open(cls, filename):
        ext = filename.rsplit('.', 1)[-1]
        if ext == 'png':
            decoder = PNGImageDecoder
        elif ext in ('jpg', 'jpeg'):
            decoder = JPEGImageDecoder
        elif ext == 'gif':
            decoder = GIFImageDecoder
        else:
            raise RuntimeError('Невозможно декодировать файл %s' % filename)
        byterange = decoder.decode(filename)
        return cls(byterange, filename)

    def __init__(self, byterange, filename):
        self._byterange = byterange
        self._filename = filename


Image.open('picture.png')  # PNG decode
Image.open('picture.jpg')  # JPEG decode
Image.open('picture.gif')  # GIF decode
```

Еще пример

```python
"""
*What is this pattern about?
Define a family of algorithms, encapsulate each one, and make them interchangeable.
Strategy lets the algorithm vary independently from clients that use it.
*TL;DR
Enables selecting an algorithm at runtime.
"""


class Order:
    def __init__(self, price, discount_strategy=None):
        self.price = price
        self.discount_strategy = discount_strategy

    def price_after_discount(self):
        if self.discount_strategy:
            discount = self.discount_strategy(self)
        else:
            discount = 0
        return self.price - discount

    def __repr__(self):
        fmt = "<Price: {}, price after discount: {}>"
        return fmt.format(self.price, self.price_after_discount())


def ten_percent_discount(order):
    return order.price * 0.10


def on_sale_discount(order):
    return order.price * 0.25 + 20


def main():
    """
    >>> Order(100)
    <Price: 100, price after discount: 100>
    >>> Order(100, discount_strategy=ten_percent_discount)
    <Price: 100, price after discount: 90.0>
    >>> Order(1000, discount_strategy=on_sale_discount)
    <Price: 1000, price after discount: 730.0>
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

#### Шаблонный метод (Template method)

Паттерн Шаблонный метод позволяет определить шаги алгоритма, оставив реализацию некоторых шагов подклассам.

Паттерн Шаблонный метод в некоторых отношениях похож на паттерн Мост.

```python
"""
Шаблонный метод (Template method) - паттерн поведения классов.
Шаблонный метод определяет основу алгоритма и позволяет подклассам переопределить некоторые шаги алгоритма,
не изменяя его структуру в целом.
"""


class ExampleBase(object):
    def template_method(self):
        self.step_one()
        self.step_two()
        self.step_three()

    def step_one(self):
        raise NotImplementedError()

    def step_two(self):
        raise NotImplementedError()

    def step_three(self):
        raise NotImplementedError()


class Example(ExampleBase):
    def step_one(self):
        print 'Первый шаг алгоритма'

    def step_two(self):
        print 'Второй шаг алгоритма'

    def step_three(self):
        print 'Третий шаг алгоритма'


example = Example()
example.template_method()

# Первый шаг алгоритма
# Второй шаг алгоритма
# Третий шаг алгоритма
```

Еще пример

```python
"""
An example of the Template pattern in Python
*TL;DR
Defines the skeleton of a base algorithm, deferring definition of exact
steps to subclasses.
*Examples in Python ecosystem:
Django class based views: https://docs.djangoproject.com/en/2.1/topics/class-based-views/
"""


def get_text():
    return "plain-text"


def get_pdf():
    return "pdf"


def get_csv():
    return "csv"


def convert_to_text(data):
    print("[CONVERT]")
    return "{} as text".format(data)


def saver():
    print("[SAVE]")


def template_function(getter, converter=False, to_save=False):
    data = getter()
    print("Got `{}`".format(data))

    if len(data) <= 3 and converter:
        data = converter(data)
    else:
        print("Skip conversion")

    if to_save:
        saver()

    print("`{}` was processed".format(data))


def main():
    """
    >>> template_function(get_text, to_save=True)
    Got `plain-text`
    Skip conversion
    [SAVE]
    `plain-text` was processed
    >>> template_function(get_pdf, converter=convert_to_text)
    Got `pdf`
    [CONVERT]
    `pdf as text` was processed
    >>> template_function(get_csv, to_save=True)
    Got `csv`
    Skip conversion
    [SAVE]
    `csv` was processed
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

#### Посетитель (Visitor)

Паттерн Посетитель используется, когда нужно применить некую функцию к каждому элементу коллекции или объекту-агрегатору. Это не то же самое, что типичное использование паттерна Итератор - где мы обходим коллекцию или агрегат и вызываем некий метод для каждого элемента, - поскольку в случае "посетителя" вызывается внешнняя функция, а не метод.

В Python имеется встроенная поддержва этого паттерна. Например конструкция `new_list = map(function, old_sequence)` означает, что `function()` вызывается для каждого элемента `old_sequence`, в результате чего порождается `new_list`

```python
"""
Постетитель (Visitor) - паттерн поведения объектов.
Описывает операцию, выполняемую с каждым объектом из некоторой структуры.
Паттерн посетитель позволяет определить новую операцию, не изменяя классы этих объектов.
"""


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

Еще пример

```python
"""
http://peter-hoffmann.com/2010/extrinsic-visitor-pattern-python-inheritance.html
*TL;DR
Separates an algorithm from an object structure on which it operates.
An interesting recipe could be found in
Brian Jones, David Beazley "Python Cookbook" (2013):
- "8.21. Implementing the Visitor Pattern"
- "8.22. Implementing the Visitor Pattern Without Recursion"
*Examples in Python ecosystem:
- Python's ast.NodeVisitor: https://github.com/python/cpython/blob/master/Lib/ast.py#L250
which is then being used e.g. in tools like `pyflakes`.
- `Black` formatter tool implements it's own: https://github.com/ambv/black/blob/master/black.py#L718
"""


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

#### Поведенческие паттерны. Итог

Для некоторых поведенческих паттернов в Python имеется прямая поддержка; остальные нетрудно реализовать самостоятельно. Паттерны Цепочка ответственности, Посредник и Наблюдатель можно реализовать традиционным способом или с помощью сопрограмм, и все они являются вариациями на тему разрыва связи между взаимодействующими объектами. Паттерн Команда можно использовать для отложенного вычисления и реализации механизма выполнения-отмена. Поскольку Python - интерпретируемый язык (на уровне байт-кода), то паттерн Интерпретатор можно реализовать с помощью самого Python и даже изолировать интерпретируемый код в отдельном процессе. Поддержка паттерна Итератор (и - неявно - паттерна посетитель) встроена в Python. Паттерн Хранитель неплохо поддержан в стандартной библиотеке Python (например, с помощью модулей `pickle` и `json`). У паттернов Состояние, Стратегия и Шаблонный метод прямой поддержки нет, но все они легко реализуются.

## Что такое lru cache

- [LRU, метод вытеснения из кэша](https://habr.com/ru/post/136758/)

LRU (least recently used) — это алгоритм, при котором вытесняются значения, которые дольше всего не запрашивались. Соответственно, необходимо хранить время последнего запроса к значению. И как только число закэшированных значений превосходит N необходимо вытеснить из кеша значение, которое дольше всего не запрашивалось.
