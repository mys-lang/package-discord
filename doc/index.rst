|discord|_
|test|_
|stars|_

About
=====

A Discord client in the `Mys programming language`_.

Project: https://github.com/mys-lang/package-discord

Examples
========

.. code-block:: mys

   from discord import Client
   from discord import Handler

   class MyHandler(Handler):

       def on_message(self, message: Message, client: Client):
           if message.author == client.user:
               return

           if message.content == "!hello":
               message.channel.send("Hello!")

   def main():
       client = Client(MyHandler())
       client.run("your token here")

API
===

.. mysfile:: src/lib.mys

.. |discord| image:: https://img.shields.io/discord/777073391320170507?label=Discord&logo=discord&logoColor=white
.. _discord: https://discord.gg/GFDN7JvWKS

.. |test| image:: https://github.com/mys-lang/package-discord/actions/workflows/pythonpackage.yml/badge.svg
.. _test: https://github.com/mys-lang/package-discord/actions/workflows/pythonpackage.yml

.. |stars| image:: https://img.shields.io/github/stars/mys-lang/package-discord?style=social
.. _stars: https://github.com/mys-lang/package-discord

.. _Mys programming language: https://mys.readthedocs.io/en/latest/
