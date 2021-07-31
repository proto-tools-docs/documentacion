Ejemplos
========

Ejemplo 01
----------

Prototipado de una calculador simple.

.. code-block:: python

   from prototools.menu import EzMenu
   from prototools.utils import entradas

   mensajes = ("Ingresar primer numero: ", "Ingresar segundo numero: ")

   def suma():
       x, y = entradas(mensajes)
       print(x + y)

   def resta():
       x, y = entradas(mensajes)
       print(x - y)

   def multiplicacion():
       x, y = entradas(mensajes)
       print(x * y)

   def division():
       x, y = entradas(mensajes)
       try:
           print(x/y)
       except ZeroDivisionError:
           print("No es divisible")

   menu = EzMenu()
   menu.agregar_opciones("sumar", "restar", "multiplicar", "dividir", "salir")
   menu.agregar_funcion(suma, 1)
   menu.agregar_funcion(resta, 2)
   menu.agregar_funcion(multiplicacion, 3)
   menu.agregar_funcion(division, 4)
   menu.run()

.. tip::
   Tambien puedes usar `agregar_funciones( )` para agregar todas las funciones

   .. code-block:: python

      menu.agregar_funciones(suma, resta, multiplicacion, division)

   Usando esta forma, es esencial el orden en el que agregegas las funciones que 
   serán mapeadas a las opciones del menú.

Ejemplo 02
----------

Prototipado simple de un cajero automático.

.. code-block:: python

   from prototools.menu import EzMenu
   from prototools.variable import Cuenta

   mi_cuenta = Cuenta('1234', 1000)

   def depositar():
       monto = float(input("Ingresar cantidad a depositar: "))
       mi_cuenta.saldo += monto

   def retirar():
       monto = float(input("Ingresar cantidad a retirar: "))
       if monto > 0 and mi_cuenta.saldo > monto:
           mi_cuenta.saldo -= monto
       else:
           print("No tiene suficiente saldo")

   def saldo():
       print(f"Saldo actual: {mi_cuenta.saldo}")

   menu = EzMenu()
   menu.titulo("Bienvenido a su ATM")
   menu.agregar_opciones("depositar", "retirar", "saldo", "salir")
   menu.agregar_funcion(depositar, 1)
   menu.agregar_funcion(retirar, 2)
   menu.agregar_funcion(saldo, 3)
   menu.run()
