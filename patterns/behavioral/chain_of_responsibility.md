## Цепочка ответственности (Chain of responsobility)

Паттерн цепочка ответственности предназначен, для того чтобы разорвать связь между отправителем запроса и получателем, который этот запрос обрабатывает. Вместо непосредственного вызова одной функции из другой первая функция отправляет запрос цепочке получателей. Первый получатель в цепочке может либо обработать запрос и прервать цепочку (не передавая запрос дальше), либо передать запрос следующему получателю. У второго получателя есть такой же выбор и так далее, пока запрос не дойдет до последнего получателя (который может отбросить запрос или возбудить исключение).

Представьте себе пользовательский интерфейс, который получает события для обработки. Одни события поступают от пользователя (например, события мыши и клавиатуры), другие - от системы (например, события таймера).

### Пример 1:
```python

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

### Пример 2:
```python
class HttpHandler(object):
    """Абстрактный класс обработчика"""
    def handle(self, code):
        raise NotImplementedError()


class Http404Handler(HttpHandler):
    """Обработчик для кода 404"""
    def handle(self, code):
        if code == 404:
            return 'Страница не найдена'


class Http500Handler(HttpHandler):
    """Обработчик для кода 500"""
    def handle(self, code):
        if code == 500:
            return 'Ошибка сервера'


class Client(object):
    def __init__(self):
        self._handlers = []

    def add_handler(self, h):
        self._handlers.append(h)

    def response(self, code):
        for h in self._handlers:
            msg = h.handle(code)
            if msg:
                print 'Ответ: %s' % msg
                break
        else:
            print 'Код не обработан'


client = Client()
client.add_handler(Http404Handler())
client.add_handler(Http500Handler())
client.response(400)  # Код не обработан
client.response(404)  # Ответ: Страница не найдена
client.response(500)  # Ответ: Ошибка сервера
```