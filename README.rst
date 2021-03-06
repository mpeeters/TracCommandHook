TracCommandHook
===============

``TracCommandHook`` is a Trac plugin that executes a specified command after
ticket creation or modification. The command is called only if the ticket
is created with (or changed to) one or more specified priorities.

It has been tested on `Trac 0.12 <http://trac.edgewall.org>`_.


Configuration
-------------

The command and its options must be specified in trac.ini : ::

    [commandhook]
    section = commandhookgrowl,commandhookirc

    [commandhookgrowl]
    command = /usr/local/bin/growlnotify
    priorities = blocker
    param.title-parameter = -t
    param.title-fields = summary
    param.message-parameter = -m
    param.message-fields = id," ",priority," ","new ticket" 

    [commandhookirc]
    priorities = blocker
    command = affinitic.ircutils/bin/send_irc_message,unnamedparam1,unnamedparam2
    param.server-parameter = -s
    param.server-fields = "irc.freenode.net"
    param.port-parameter = -p
    param.port-fields = "6667"
    param.nickname-parameter = -n
    param.nickname-fields = "BotNickname"
    param.channel-parameter = -c
    param.channel-fields = "#ourchannel"
    param.message-parameter = -m
    param.message-fields = "${trac:project-url}/ticket/",id," A new ticket"," ",priority," has been created by"," ",reporter,": ",summary," assigned to: ",owner


In this example, when a ticket (#1) with priority blocker is created or
modified, the following command will be executed (first part of the example
above; the second command will of course be executed as well) : ::

    /usr/local/bin/growlnotify -t 'Summary of the ticket' -m '1 blocker new ticket'

"" in -fields allow to return hard value, that value will be displayed without the ""


Details
-------

``priorities`` is a list of priorities, ex : ``blocker`` or ``blocker,critical``.

Command parameters can be defined using ``param.`` notation : 
 - ``param.*-fields`` is a list of ticket fields (ex : id, summary, priority,
   owner, ...) which will be joined into a string
 - ``param.*-parameter`` is the command parameter that will receive the
   constructed string

Replace the ``*`` by the identifier you like, once for each parameter you want
to pass to the command.


Credits
-------

This package was developed by `Affinitic team <https://github.com/affinitic>`_.

.. image:: http://www.affinitic.be/affinitic_logo.png
   :alt: Affinitic website
   :target: http://www.affinitic.be

``TracCommandHook`` is licensed under GNU General Public License, version 2.


**Enjoy and improve !**
