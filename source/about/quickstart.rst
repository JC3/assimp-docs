.. _ai_main_data:

Data Structures
---------------

When the importer successfully completed its job, the imported data is returned in an aiScene structure. This is the root
point from where you can access all the various data types that a scene/model file can possibly contain. The
:ref:`ai_data` describes how to interpret this data.

.. _ai_ext:

Extending the library
---------------------

There are many 3d file formats in the world, and we're happy to support as many as possible. If you need support for
a particular file format, why not implement it yourself and add it to the library? Writing importer plugins for
assimp is considerably easy, as the whole postprocessing infrastructure is available and does much of the work for you.
See the :ref:`ai_extend` extend Extending the library @endlink page for more information.


.. _ai_main_support:

Support & Feedback
------------------

If you have any questions/comments/suggestions/bug reports you're welcome to post them in our
`Github-Issue-Tracker <https://github.com/assimp/assimp/issues>`_. Alternatively there's
a mailing list, `assimp-discussions <https://github.com/assimp/assimp/discussions>`_
.

.. _ai_install_prebuilt:

Using the pre-built libraries with Visual-Studio
------------------------------------------------

If you develop at Visual Studio 2015, 2017 or 2019, you can simply use the pre-built linker libraries provided in the distribution.
Extract all files to a place of your choice. A directory called "assimp" will be created there. Add the assimp/include path
to your include paths (Menu-&gt;Extras-&gt;Options-&gt;Projects and Solutions-&gt;VC++ Directories-&gt;Include files)
and the assimp/lib/&lt;Compiler&gt; path to your linker paths (Menu-&gt;Extras-&gt;Options-&gt;Projects and Solutions-&gt;VC++ Directories-&gt;Library files).
This is necessary only once to setup all paths inside you IDE.

To use the library in your C++ project you can simply generate a project file via cmake. One way is to add the assimp-folder 
as a subdirectory via the cmake-command

::

    ADD_SUBDIRECTORY(assimp)

Now just add the assimp-dependency to your application:

::

    TARGET_LINK_LIBRARIES(my_game assimp)


If done correctly you should now be able to compile, link, run and use the application. 

.. _ai_install_prebuilt_vcpg:

Build on all platforms using vcpkg
----------------------------------

You can download and install assimp using the `vcpkg <https://github.com/Microsoft/vcpkg/>`_ dependency manager:
::

    bash
    git clone https://github.com/Microsoft/vcpkg.git
    cd vcpkg
    ./bootstrap-vcpkg.sh
    ./vcpkg integrate install
    vcpkg install assimp

The assimp port in vcpkg is kept up to date by Microsoft team members and community contributors. If the version is out of date, please <reate an issue or pull request on the `vcpkg repository <https://github.com/Microsoft/vcpkg>`_ .


.. _ai_install_own:

Building the library from scratch
---------------------------------

First you need to install cmake. Now just get the code from github or download the latest version from the webside.
to build the library just open a command-prompt / bash, navigate into the repo-folder and run cmake via:

::

    cmake CMakeLists.txt

A project-file of your default make-system ( like gnu-make on linux or Visual-Studio on Windows ) will be generated. 
Run the build and you are done. You can find the libs at assimp/lib and the dll's / so's at bin.

.. _ai_assimp_dll:

Windows DLL Build
-----------------

The Assimp-package can be built as DLL. You just need to run the default cmake run.


.. _ai_andorid_build:

The Android build
-----------------

This module provides a facade for the io-stream-access to files behind the android-asset-management within 
an Android-native application.
- It is built as a static library
- It requires Android NDK with android API > 9 support.

Building
----------------
To use this module please provide following cmake defines:

::

    -DASSIMP_ANDROID_JNIIOSYSTEM=ON
    -DCMAKE_TOOLCHAIN_FILE=$SOME_PATH/android.toolchain.cmake
    
"SOME_PATH" is a path to your cmake android toolchain script.

The build script for this port is based on `Android-CMake <https://github.com/taka-no-me/android-cmake>`_.  
See its documentation for more Android-specific cmake options (e.g. -DANDROID_ABI for the target ABI).

Code
--------
A small example how to wrap assimp for Android:

::

    #include <assimp/port/AndroidJNI/AndroidJNIIOSystem.h>

    Assimp::Importer* importer = new Assimp::Importer();
    Assimp::AndroidJNIIOSystem *ioSystem = new Assimp::AndroidJNIIOSystem(app->activity);
    if ( nullptr != iosSystem ) {
      importer->SetIOHandler(ioSystem);
    }  

The Assimp-package can be built as DLL. You just need to run the default cmake run.

.. _ai_static_lib:

Assimp static lib
-----------------

The Assimp-package can be build as a static library as well. Do do so just set the configuration variable **BUILD_SHARED_LIBS**
to off during the cmake run.
