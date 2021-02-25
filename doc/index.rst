About
=====

A Discord client in the `Mys programming language`_.

Project: https://github.com/mys-lang/package-discord

Examples
========

.. code-block:: python

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

Functions and types
===================

.. mysfile:: src/lib.mys

.. _Mys programming language: https://mys.readthedocs.io/en/latest/
