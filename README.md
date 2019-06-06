# vcpkg-manual-downloading

Vcpkg install often fails due to very slow downloading of the source package. We can download the source package file manually and then continue the installation. 

## Case 1: vcpkg_from_github 

For some packages, vcpkg downloding is instructed via vcpkg_from_github.  For example, in vcpkg/ports/assimp/portfile.cmake, we can find the following information

```
vcpkg_from_github(
    OUT_SOURCE_PATH SOURCE_PATH
    REPO assimp/assimp
    REF v4.1.0
    SHA512 5f1292de873ae16c9921d1d44f2871474d74c0ddfd76cc928a7d9b3e03aa6eca4cc72af0513da20a86d09c55d48646e610fd4a4f2b05364f08ad09cf27cbc67a
    HEAD_REF master
    PATCHES
        dont-overwrite-prefix-path.patch
        uninitialized-variable.patch
)
```


* Determine the URL of the source package

Go to the release page of assimp v4.1.0: https://github.com/assimp/assimp/releases/tag/v4.1.0 , we can find the url should be https://github.com/assimp/assimp/archive/v4.1.0.tar.gz 

* Download the source package manually, and save it to vcpkg/download/assimp-assimp-v4.1.0.tar.gz   . The filename of the saved file: assimp-assimp-v4.1.0.tar.gz is constructed by two words in REPO sectionn and the original filename.

* Run vcpkg install , you will get an error message complaining that the actual hash is not the same as the expected hash in portfile.cmake . You can simply edit portfile.cmake to replace the expected hash with the actual one.

* Run vcpkg install again.
 
