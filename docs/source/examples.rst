Examples
========

Example 01
----------

A simple calculator.

.. code-block:: python

    from prototools import Menu, float_input


    def _user_input(f):
        x = float_input("First number: ")
        y = float_input("Second number: ")
        print(f"Result: {f(x, y)}")


    def addition(x, y):
        return x + y


    def substraction(x, y):
        return x - y


    def multiplication(x, y):
        return x * y


    def division(x, y):
        try:
            return x / y
        except ZeroDivisionError:
            return "Can't divide by zero"


    def about():
        print("Just Another Simple Calculator")


    def main():
        menu = Menu()
        menu.add_options(
            ("Addition", lambda: _user_input(addition)),
            ("Substraction", lambda: _user_input(substraction)),
            ("Multiplication", lambda: _user_input(multiplication)),
            ("Division", lambda: _user_input(division)),
            ("About", about),
        )
        menu.run()


    if __name__ == "__main__":
        main()


::

            ┌─────────────────────────────────────────────────────┐
            │                                                     │
            │                          Menu                       │
            │                                                     │
            │                                                     │
            │  1 - Addition                                       │
            │  2 - Substraction                                   │
            │  3 - Multiplication                                 │
            │  4 - Division                                       │
            │  5 - About                                          │
            │  6 - Exit                                           │
            │                                                     │
            │                                                     │
            └─────────────────────────────────────────────────────┘
            >


Example 02
----------

Temperature converter.

.. code-block:: python

    from prototools import Menu, float_input


    def datos(msg, f):
        data = float_input(msg)
        print(f(data))


    def fahrenheit_to_celsius(F):
        return (F - 32) * (5/9)


    def celsius_to_fahrenheit(C):
        return (C * 9/5) + 32


    def main():
        menu = Menu("Temperature Converter")
        menu.add_options(
            ("Fahrenheit to Celsius",
            lambda: datos("Temperature (°F): ", fahrenheit_to_celsius)),
            ("Celsius to Fahrenheit",
            lambda: datos("Temperature (°C): ", celsius_to_fahrenheit)),
            ("Test", lambda x: print(celsius_to_fahrenheit(x)), 2)
        )
        menu.run()


    if __name__ == "__main__":
        main()


::

            ┌─────────────────────────────────────────────────────────┐
            │                                                         │
            │                Conversor de Temperatura                 │
            │                                                         │
            │                                                         │
            │  1 - Fahrenheit para Celsius                            │
            │  2 - Celsius para Fahrenheit                            │
            │  3 - Test                                               │
            │  4 - Exit                                               │
            │                                                         │
            │                                                         │
            └─────────────────────────────────────────────────────────┘
            >


Example 03
----------

Menu with options, one of them a Quadratic equation solver.

.. code-block:: python

    from cmath import sqrt
    from prototools import Menu, int_input

    sol1 = lambda a, b, c: (-b + sqrt(b ** 2 - 4 * a * c)) / (2 * a)
    sol2 = lambda a, b, c: (-b - sqrt(b ** 2 - 4 * a * c)) / (2 * a)
    sol = lambda a, b, c: (sol1(a, b, c), sol2(a, b, c))
    area, sum_sqrt = lambda b, h: b * h / 2, lambda x, y: (x + y) ** 0.5


    def main():
        menu = Menu()
        menu.add_options(
            (
                "Square root of the sum of two numbers",
                lambda: print(sum_sqrt(
                    int_input("First number: "),
                    int_input("Second number: "),
                ))),
            (
                "Quadratic equation solver",
                lambda: print(sol(
                    int_input("Coefficient a: "),
                    int_input("Coefficient b: "),
                    int_input("Coefficient c: "),
                ))),
            (
                "Area of Rectangle",
                lambda: print(area(
                    int_input("Base: "),
                    int_input("Height: "),
                ))),
        )
        menu.run()


    if __name__ == "__main__":
        main()


::

            ┌───────────────────────────────────────────────────────────────┐
            │                                                               │
            │                            Menu                               │
            │                                                               │
            │                                                               │
            │  1 - Square root of the sum of two numbers                    │
            │  2 - Quadratic equation solver                                │
            │  3 - Area of Rectangle                                        │
            │  4 - Exit                                                     │
            │                                                               │
            │                                                               │
            └───────────────────────────────────────────────────────────────┘
            >


Example 04
----------

Menu, Submenu and Items.

.. code-block:: python

    from prototools.menu import Menu, FunctionItem, Submenu
    from prototools.components import Box, render
    from prototools.colorize import red, blue, yellow


    version = "Current version: 0.1.6" 

    contributors = [
        "Guido Van Rossum",
        "Tim Peters",
        "Adrian Holovaty",
        "Jacob Kaplan-Moss",
        "Wes McKinney",
        "Pauli Virtanen",
        "Armin Ronacher",
    ]

    libraries = [
        "Requests",
        "BeutifulSoup",
        "Django",
        "Flask",
        "SQLAlchemy",
        "NumPy",
        "Pandas",
        "Matplotlib",
        "OpenCV",
        "Pillow",
        "PyGame",
        "TensorFlow",
        "NLTK",
        "Scipy",
    ]

    text = """\
        Beautiful is better than ugly.
        Explicit is better than implicit.
        Simple is better than complex.
        Complex is better than complicated.
        Flat is better than nested.
        Sparse is better than dense.
        Readability counts.
        Special cases aren't special enough to break the rules.
        Although practicality beats purity.
        Errors should never pass silently.
        Unless explicitly silenced.
        In the face of ambiguity, refuse the temptation to guess.
        There should be one-- and preferably only one --obvious way to do it.
        Although that way may not be obvious at first unless you're Dutch.
        Now is better than never.
        Although never is often better than *right* now.
        If the implementation is hard to explain, it's a bad idea.
        If the implementation is easy to explain, it may be a good idea.
        Namespaces are one honking great idea -- let's do more of those!
    """

    def zen():
        render(Box(textnl=text))
        input()

    def show(text):
        if isinstance(text, str):
            print(text)
        else:
            for line in text:
                print(line)
        input()


    menu = Menu(red("Prototools"), arrow_keys=True)

    menu_zen = Menu(yellow("Zen of Python"), exit_option_text="Back")
    menu_zen.add_item(FunctionItem("Show zen", zen))

    menu_users = Menu(blue("Contributors"), exit_option_text="Back")
    menu_users.add_item(FunctionItem("List of contributors", show, kwargs={"text": contributors}))

    options = (
        Submenu("The Zen of Python", submenu=menu_zen),
        Submenu("Python Contributors", submenu=menu_users),
        FunctionItem("Libraries", show, kwargs={"text": libraries}),
        FunctionItem("Prototools version", show, kwargs={"text": version}),
    )

    menu.add_items(options)
    menu.run()


::

            ┌─────────────────────────────────────────────────────────────────────────┐
            │                                                                         │
            │                               Prototools                                │
            │                                                                         │
            │                                                                         │
            │  1 - The Zen of Python                                                  │
            │  2 - Python Contributors                                                │
            │  3 - Libraries                                                          │
            │  4 - Prototools version                                                 │
            │  5 - Exit                                                               │
            │                                                                         │
            │                                                                         │
            └─────────────────────────────────────────────────────────────────────────┘
            Prototools| The Zen of Python