## Декоратор (Decorator)

Декоратором называется функция, которая принимает функцию с таким же именем, как у исходной, но с расширенной функциональностью. Декораторы часто используются во фреймвоках, чтобы упростить интеграцию пользовательских функций с фреймворком.

Паттерн Декоратор настолько полезен, что в Python встроена специальная поддержка для него. В Python декорировать можно как функции, так и методы. Кроме того, Python поддерживает декораторы классов: функции, которые принимают класc в качестве аргумента и возвращают новый класс с таким же именем, как у исходного, но дополненной функциональностью.

Иногда декораторы классов удобно использовать как альтернативу производным классам.

### Пример 1 :
```python
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

### Пример 2:
```python
class Man(object):
    """Человек"""
    def __init__(self, name):
        self._name = name

    def say(self):
        print 'Привет! Меня зовут %s!' % self._name


class Jetpack(object):
    """Реактивный ранец"""
    def __init__(self, man):
        self._man = man

    def __getattr__(self, item):
        return getattr(self._man, item)

    def fly(self):
        # расширяем функциональность объекта добавляя возможность летать
        print '%s летит на реактивном ранце!' % self._man._name


man = Man('Виктор')

man_jetpack = Jetpack(man)
man_jetpack.say()  # Привет! Меня зовут Виктор!
man_jetpack.fly()  # Виктор летит на реактивном ранце!
```

### Пример 3:
```python
# Основная функция, которую будем декорировать
def greet(name):
    return f"Hello, {name}!"

# Декоратор, который добавляет дополнительное сообщение
def excited_decorator(func):
    def wrapper(name):
        return func(name) + " :)"
    return wrapper

# Декоратор, который добавляет приветствие перед функцией
def formal_decorator(func):
    def wrapper(name):
        return "Good evening, " + func(name)
    return wrapper

# Применяем декораторы
greet_excited = excited_decorator(greet)
greet_formal = formal_decorator(greet)

# Использование декорированных функций
print(greet("Alice"))         # Hello, Alice!
print(greet_excited("Alice")) # Hello, Alice! :)
print(greet_formal("Alice"))  # Good evening, Hello, Alice!

```

### Пример 4:
```python
@excited_decorator
@formal_decorator
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))  # Good evening, Hello, Alice! :)

```