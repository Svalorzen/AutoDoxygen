Auto-Doxygen
============

This is a project that allows you to painlessly setup Doxygen for your C++
repository, while using [Doxygen Awesome](https://github.com/jothepro/doxygen-awesome-css)
to create a visually appealing documentation.

The specific settings used are not really meant to be configured; if you want to
change them feel free to fork this repo for your own usage.

Simply add to your main `CMakeLists.txt` file the following:
```
set(AUTODOXY_HEADER_DIR "include")
CPMAddPackage(
    GITHUB_REPOSITORY "svalorzen/AutoDoxygen"
    GIT_TAG "main"
)
```
Remember to set `AUTODOXY_HEADER_DIR` to the name of the folder (from your
`SOURCE_DIR`) that contains the header files to document!
