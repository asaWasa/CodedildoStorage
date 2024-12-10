## Посредник (Mediator)

Паттерн Посредник представляет средства для создания объекта - посредника - который инкапсулирует взаимодействия между другими объектами. Это позволяет осуществлять взаимодействия между объектами, которые ничего не знают друг о друге. Например, в случае нажатия кнопки соответствующий ей объект должен только известить посредника, а уж тот уведомит все объекты, которых интересует нажатие этой кнопки.

Посредник обеспечивает слабую [связанность](/interview/questions/oop.md#coupling) системы, избавляя объекты от необходимости явно ссылаться друг на друга и позволяя тем самым независимо изменять взаимодействия между ними.

### Пример 1:
```python
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

### Пример 2:
```python
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
