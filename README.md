# github.com/ALTUSNETS\

The source tree contains the Device Tree Compiler (dtc) toolchain for
working with device tree source and binary files and also libfdt, a
utility library for reading and manipulating the binary format.

DTC and LIBFDT are maintained by:

David Gibson <david@gibson.dropbear.id.au>
Jon Loeliger <jdl@jdl.com>


Python library
--------------

A Python library is also available. To build this you will need to install
swig and Python development files. On Debian distributions:

   sudo apt-get install swig python-dev

The library provides an Fdt class which you can use like this:

$ PYTHONPATH=../pylibfdt python
>>> import libfdt
>>> fdt = libfdt.Fdt(open('test_tree1.dtb').read())
>>> node = fdt.path_offset('/subnode@1')
>>> print node
124
>>> prop_offset = fdt.first_property_offset(node)
>>> prop = fdt.get_property_by_offset(prop_offset)
>>> print '%s=%r' % (prop.name, prop.value)
compatible=bytearray(b'subnode1\x00')
>>> print '%s=%s' % (prop.name, prop.value)
compatible=subnode1
>>> node2 = fdt.path_offset('/')
>>> print fdt.getprop(node2, 'compatible')
test_tree1

You will find tests in tests/pylibfdt_tests.py showing how to use each
method. Help is available using the Python help command, e.g.:

    $ cd pylibfdt
    $ python -c "import libfdt; help(libfdt)"

If you add new features, please check code coverage:

    $ sudo apt-get install python-pip python-pytest
    $ sudo pip install coverage
    $ cd tests
    $ coverage run pylibfdt_tests.py
    $ coverage html
    # Open 'htmlcov/index.html' in your browser


To install the library via the normal setup.py method, use:

    ./pylibfdt/setup.py [--prefix=/path/to/install_dir]

If --prefix is not provided, the default prefix is used, typically '/usr'
or '/usr/local'. See Python's distutils documentation for details. You can
also install via the Makefile if you like, but the above is more common.

To install both libfdt and pylibfdt you can use:

    make install [SETUP_PREFIX=/path/to/install_dir] \
            [PREFIX=/path/to/install_dir]

To disable building the python library, even if swig and Python are available,
use:

    make NO_PYTHON=1


More work remains to support all of libfdt, including access to numeric
values.


Mailing list
------------
The following list is for discussion about dtc and libfdt implementation
mailto:devicetree-compiler@vger.kernel.org

Core device tree bindings are discussed on the devicetree-spec list:
mailto:devicetree-spec@vger.kernel.org
