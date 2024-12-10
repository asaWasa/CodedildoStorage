## Стратегия (Strategy)

Паттерн Стратегия позволяет инкапсулировать набор взаимозаменяемых алгоритмов, из которых пользователь выбирает тот, что ему нужен.

### Пример 1:
```python
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

### Пример 2:
```python
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

