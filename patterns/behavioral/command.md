## Команда (Command)

Паттерн Команда применяется для инкапсуляции команд в виде объектов. Например, с его помощью можно построить последовательность команд для отложенного выполнения или создать команды, допускающие отмену.

### Пример 1:
```python
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

### Пример 2:
```python
class Light(object):
    def turn_on(self):
        print 'Включить свет'

    def turn_off(self):
        print 'Выключить свет'


class CommandBase(object):
    def execute(self):
        raise NotImplementedError()


class LightCommandBase(CommandBase):
    def __init__(self, light):
        self.light = light


class TurnOnLightCommand(LightCommandBase):
    def execute(self):
        self.light.turn_on()


class TurnOffLightCommand(LightCommandBase):
    def execute(self):
        self.light.turn_off()


class Switch(object):
    def __init__(self, on_cmd, off_cmd):
        self.on_cmd = on_cmd
        self.off_cmd = off_cmd

    def on(self):
        self.on_cmd.execute()

    def off(self):
        self.off_cmd.execute()


light = Light()
switch = Switch(on_cmd=TurnOnLightCommand(light),
                off_cmd=TurnOffLightCommand(light))
switch.on()  # Включить свет
switch.off()  # Выключить свет
```