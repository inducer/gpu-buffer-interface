OpenCL/CUDA Buffer Interface
============================

Python interface
----------------

.. {{{

This document specifies an object as implementing the buffer interface by
having a number of attributes and methods. If an implementation chooses to
implement the buffer interface as a temporary view, the way to obtain the
object implementing the :class:`BufferInterface` is implementation-defined.
The user may call :meth:`BufferInterface.release` to explicitly release any
resources associated with the view.

.. class:: BufferInterface

    .. attribute:: buffer

        *OpenCL:* An object that has a ``int_ptr`` attribute which is a :class:`int`
        representing the ``cl_mem`` pointer.

        *CUDA:* An object that is castable to an :class:`int` representing
        the numerical value of the CUDA device pointer.

    .. attribute:: offset

        *OpenCL:* Relative offset from the beginning of :attr`buffer`
        to the start of the array data.

        *CUDA:* Always zero.

    .. todo::

        We should also define a way to access a host pointer for the
        relevant memory area, if available.

    .. attribute:: dtype

        .. todo::

            What type system? :class:`numpy.dtype`? `lltypes <https://github.com/ContinuumIO/lltypes>`_?

    .. attribute:: shape

        A shape tuple, just like :attr`numpy.ndarray.shape`.

    .. attribute:: strides

        A strides tuple, just like :attr`numpy.ndarray.strides`.

    .. attribute:: strides

        A strides tuple, just like :attr`numpy.ndarray.strides`.

    .. method:: release()

        If *self* is a proxy to the actual object holding the data then
        either garbage collection or an explicit `release` call will free
        the resources occupied by the proxy. Otherwise, this method is a
        no-op.


.. note::

    I don't think it's appropriate for the interface to mandate the use of
    :mod:`pyopencl` or :mod:`pycuda`. It's of course intended that the
    interface play well with the two, but I believe this is about
    specifying an interface, not an implementation. That's how I arrived at
    the spec above.

.. }}}

CPython interface
-----------------

.. {{{

.. todo::

    I would suggest that the CPython-specific interface be as minimal as
    possible, just providing a hatch to get to the low-level C interface.

.. }}}

C interface
-----------

.. {{{

.. todo::

    Frédéric/Arnaud--could you paste in the interface that your array object
    obeys as a starting point?

.. }}}

.. vim: foldmethod=marker:sw=4:textwidth=75
