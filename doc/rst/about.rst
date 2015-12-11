About
=====

This document provides a basic overview of MTools.

Background
----------

The story of MTools (and why it is needed) begins with the story of the Qt
C++ framework. Today, Qt5 is indisputably one of the most well designed pieces
of software ever created. Released over 20 years ago in 1995, Qt is
exceptionally well documented and architectured. Although Qt is written in C++
and intended mostly for Desktop GUI applications, Qt5 has inspired Mutant Engine
in many ways.

Event-driven programming is a natural and inherent part of any GUI application
or toolkit. Several earlier toolkits used various solutions, ranging from
callbacks (Motif), to sub-classing (WxWidgets), to macros (MFC). All of these
solutions are unwieldy and error-prone. But the biggest drawback of all was the
lack of type-safety. Qt introduced a novel solution of its own: Signals and
Slots, using a Meta-object compiler. The Qt preprocessor (moc) generates extra
information for the compiler to help the Qt runtime listen for when an object
sends a signal (emits an event), and then forwards that signal to another object
(possibly the original object that emitted the signal). Signals are received by
slots - methods that are part of the object receiving the signal. Slots work
just like if an object's method had been given as a callback for an event,
except that slots are thread-safe.

To help clarify what Signals and Slots are, consider the following pseudo-code
example: 

.. code-block:: c++

   Counter a, b;
   QObject::connect(&a, SIGNAL(valueChanged(int)), &b, SLOT(setValue(int)));
   a.setValue(12);  // a.value() == 12, b.value() == 12

In this example, we create two new objects, both ``Counter`` objects. We connect
the ``valueChanged`` signal from the first object to the ``setValue`` slot on
the second object. ``setValue`` is a member function that emits the
``valueChanged`` signal whenever it is called, so when we call ``setValue`` on
the first object, the ``valueChanged`` signal is emitted from the first object.
We connected object 1's ``valueChanged`` signal to object 2's ``setValue`` slot,
so now object 2's ``setValue`` is called with the same value that was given to
object 1 (12 in this case). If you need more help understanding Signals and
Slots, please read the Qt5 documentation at
http://doc.qt.io/qt-5/signalsandslots.html.

If you are confused by Signals and Slots, don't worry. Mutant Engine doesn't use
them. They are simply an inspiration for a different (but related) mechanism
used in Mutant Engine: The Handle.

Handles
-------

The concept of a 'handle' in computing is quite old, and presents many
advantages, if the disadvantages can be managed properly. But handles in Mutant
Engine (referred to henceforth as MHandles, to prevent confusion) are not a
replacement for callbacks, or even objects. They are a replacement for pointers.

Pointers are arguably the most powerful feature of C/C++, and are responsible
for a good portion of the efficiency for which the languages are famed. But they
come with a heavy price: They are not typesafe (and could easily be casted out
of typesafety anyway), they are capable of referencing non-existant locations
and entities, they have to be manually created and destroyed, consume resources
even when not in use if they are not destroyed, and lead to a wide variety of
programmer errors and security vulnerabilities.

In computer science, a pointer is defined as an entity which references another
entity. In this context, we will define a handle as an abstract reference to
an entity. At first, these definitions sound so similar that one may question if
handles are even needed at all. But the key word in the definition of handle is
the word *abstract*, because it applies to all interactions with that entity.
When using handles, entities are never used directly (except possibly
behind-the-scenes). Every time a user wants to use an entity, he will use the
handle, which means the user never owns or directly controls that entity. As
an example, most operating systems use handles for accessing files. The kernel
is the one who actually owns the file, and does all the reading and writing.
The application just tells the kernel it wants to use the file ``mytest.txt``,
and the kernel then gives the application a handle to reference that file (for
example, the number 33570). So if the application wanted to write the message
"hello world" to ``mytest.txt``, it would tell the kernel to write that message
to handle #33570. The application itself does not ever directly write to the
file, the kernel does. The kernel and the application use the handle to make
sure that both are refering to the same thing. One advantage of this approach
is that the result is just the same as if the application could write to the
file directly (we still have a new file named ``mytest.txt`` that has ``hello
world`` as its contents), but because the application doesn't own that file, it
is not responsible for it. If the application forgot to close the file when it
finished, the kernel would still close the file itself.

What makes handles so attractive is the fact that whoever creates the handle
is the owner of whichever resource that handle references. Suppose we were to
create a Timer object inside a function. But instead of returning the object,
we create a new Handle that references the Timer object. The Timer object
has a member named ``currentTime``, which can only be set by calling the
function ``setTimerCurrentTime(Handle, Int)``, which takes a handle to a timer
as the first parameter, and the new time to set as the second parameter. Suppose
that if ``currentTime`` were ever set to a negative number, then the entire
program will instantly crash. Even if a user called
``setTimerCurrentTime(h1, -500)``, that would still be okay.
``setTimerCurrentTime`` would check if 


.. https://en.wikipedia.org/wiki/Pointer_(computer_programming)

.. https://en.wikipedia.org/wiki/Reference_counting

.. https://en.wikipedia.org/wiki/Handle_(computing)
