# How to build pyactivemq #

# Common #
  1. `svn co https://svn.apache.org/repos/asf/activemq/activemq-cpp/trunk/activemq-cpp activemq-cpp`
  1. `svn co http://pyactivemq.googlecode.com/svn/trunk pyactivemq`

pyactivemq SVN trunk is being updated to work with ActiveMQ C++ 3.0. To use an older version of ActiveMQ C++, use pyactivemq 0.1.0.

# Fedora Core #

  1. `yum install automake autoconf libtool doxygen graphviz`
  1. `yum install e2fsprogs-devel cppunit-devel python-devel boost-devel apr-devel apr-util-devel`
  1. `cd activemq-cpp`
  1. `./autogen.sh && ./configure --prefix=/opt/activemq-cpp && make && make install`
  1. `cd ../pyactivemq`
  1. `python setup.py build`
  1. `python setup.py install` or `python setup.py bdist_rpm`

If you get the following warning when running `autogen.sh`:

```
aclocal:configure.ac:74: warning: macro `AM_PATH_CPPUNIT' not found in library
```

you need to install the `cppunit-devel` package.

If you get the following error when running `setup.py`:

```
error: invalid Python installation: unable to open /usr/lib64/python2.5/config/Makefile (No such file or directory)
```

you need to install the `python-devel` package.

You may need to edit the `include_dirs`, `library_dirs` and `extra_link_args` in `setup.py` to include the directories where you installed the ActiveMQ C++ libraries (`/opt/activemq-cpp` in the example above).

# Debian/Ubuntu #

The instructions for Ubuntu are almost identical to those for Fedora Core. Make sure you have the following packages installed prior to running `configure`:

  * libboost-python-dev
  * libcppunit-dev
  * uuid-dev

See also [pyactivemq on Ubuntu](http://www.nighttale.net/activemq/pyactivemq-on-ubuntu.html).

# Windows 2000/XP/Server 2003 #

## Boost ##
As of this writing, [Boost Consulting](http://www.boost-consulting.com/) does not provide an installer for Boost 1.36.0, so it must be compiled manually.

On 32-bit Windows, run the following command:

```
bjam --toolset=msvc address-model=32 --build-type=complete --prefix="C:\Program Files\boost\boost_1_36_0" install
```

On 64-bit Windows, run one or both of the following commands (depending on whether you also need 32-bit binaries):

```
bjam --toolset=msvc address-model=32 --build-type=complete --prefix="C:\Program Files (x86)\boost\boost_1_36_0" install
bjam --toolset=msvc address-model=64 --build-type=complete --prefix="C:\Program Files\boost\boost_1_36_0" install
```

The command should be run inside the Visual Studio Command Prompt that corresponds to your architecture.

When installing both 32-bit and 64-bit Python on Windows x64, install the 32-bit version first, to an alternate directory like `C:\Python26.x86`.

## APR ##

AMQCPP depends on the [Apache Portable Runtime](http://apr.apache.org/).

You must download and build apr, apr-util and apr-iconv on Windows.

## ActiveMQ C++ ##

AMQCPP can be compiled with Visual Studio 2008 by using the project file provided in the `win_build` directory of pyactivemq.

## pyactivemq ##

Build pyactivemq and ActiveMQ C++ using the pyactivemq solution file.

  1. Open `pyactivemq\win_build\pyactivemq.sln`.
  1. Select Build | Batch Build... from the menu.
  1. Press the Select All button.
  1. Press the Build button.

The paths in the solution are configured to allow building of 32-bit and 64-bit binaries on Windows Vista x64. You may have to change some paths to build on a different system.

A distutils `setup.py` is also included. Boost, APR and AMQCPP must be compiled before using running `setup.py`. Some useful commands:

```
C:\Python26\python.exe setup.py build
C:\Python26\python.exe setup.py bdist_wininst
C:\Python26.x86\python.exe setup.py build
C:\Python26.x86\python.exe setup.py bdist_wininst
```

# Running the broker #

ActiveMQ is a Java program, so you will need to install Sun's JRE/JDK or one of the other free alternatives to run it. I recommend using the Sun JDK.

The latest release of pyactivemq has been tested with [Apache ActiveMQ 5.2.0](http://activemq.apache.org/activemq-520-release.html).

Before running the unit tests, you should start the broker.

  1. Extract the archive.
  1. Change the working directory to `apache-activemq-5.2.0`
  1. Run `bin/activemq` (`bin\activemq.bat` on Windows).

You may have to set the `JAVA_HOME` environment variable if your Java installation is not found by the batch file.

You may want to edit the ActiveMQ script to add `-server` to `ACTIVEMQ_OPTS`, as running the broker with the Java server VM can yield improved performance. The server VM takes a while to "warm up", so it may take a few thousand messages before performance exceeds that obtained from the client VM.

# Running the unit tests #

To run the unit tests, execute `alltests.py` in the `src/test` directory. You may also wish to run `stresstests.py`, which calls the unit tests 100 times in a loop.

When running the unit tests, you might see the following error:

```
Traceback (most recent call last):
  File "alltests.py", line 20, in <module>
    from test_openwire_async import *
  File "/path/to/pyactivemq/src/test/test_openwire_async.py", line 17, in <module>
    import pyactivemq
ImportError: /usr/lib64/libboost_python.so.3: undefined symbol: PyUnicodeUCS4_FromEncodedObject
```

This can happen if you try to run the tests using a different Python installation than the one that pyactivemq and Boost.Python were compiled with.

# Source distribution #

To create source distributions, execute the command `python setup.py sdist --formats=gztar,zip`.

Make sure you have a tar command in your path.

# API documentation #

API documentation can be generated using [Epydoc](http://epydoc.sourceforge.net/):

```
PYTHONPATH=build/lib.linux-x86_64-2.5 epydoc -v --check pyactivemq
PYTHONPATH=build/lib.linux-x86_64-2.5 epydoc -v --html -o doc  pyactivemq
PYTHONPATH=build/lib.linux-x86_64-2.5 epydoc -v --pdf -o doc pyactivemq
```

When adding documentation to SVN, set the `svn:mime-type` property to `text/html` on the HTML files.