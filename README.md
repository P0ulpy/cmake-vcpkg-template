# Cmake & vcpkg template

This is a template repository made to quickly set up a project using cmake & vcpkg.
I usually use Clion as IDE so this repository have a basic .idea configuration

You can change the name of the project in the `CMakeLists.txt` and `vcpkg.json` files.

Don't forget to add your cmake generated build folder to your .gitignore !


## Setting up Git dependencies

```bash
git submodule update --init --recursive
```

__Bootstrap vcpkg :__

_Windows_
```bash
.\vcpkg\bootstrap-vcpkg.bat
```

_Unix_
```bash
.\vcpkg\bootstrap-vcpkg.sh
```

## Adding dependencies

You can add any vcpkg dependencies by editing `vcpkg.json` and then add them to you cmake target with `find_package()` and `target_link_libraries()`. You can found more information about cmake integration in the [vcpkg documentation](https://vcpkg.readthedocs.io/en/latest/users/integration/)

You can found a exemple of adding dependencies in the [Installing dependencies](#installing-dependencies) section.

## Installing dependencies

Install dependencies :

_Windows_
```bash
.\vcpkg\vcpkg.exe install --triplet x64-windows
```

_Linux_
```bash
./vcpkg/vcpkg install --triplet x64-linux
```

You can found more information about the vcpkg triplets in the [vcpkg documentation about triplets](https://learn.microsoft.com/fr-fr/vcpkg/users/triplets)

## Adding dependencies exemple with SFML :

In this exemple we will add SFML to our project, make it available in our cmake target and then compile a basic example program.

__Add dependencies to vcpkg :__

`vcpkg.json`
```json
{
  "name": "cmake-vcpkg-template",
  "version": "0.1.0",
  "builtin-baseline": "6ca56aeb457f033d344a7106cb3f9f1abf8f4e98",
  "dependencies": [
    {
      "name" : "sfml",
      "version>=" : "2.5.1#14"
    }
  ]
}
```

For further information you check the [microsoft documentation about vcpkg.json](https://learn.microsoft.com/en-us/vcpkg/reference/vcpkg-json) and [vcpkg documentation about manifests dependencies](https://vcpkg.readthedocs.io/en/latest/specifications/manifests/)

__Add dependencies to your cmake target :__

Now that we have added our dependencies to vcpkg we can add them to our cmake target.
First we use `find_package()` to find the package in vcpkg, then we use `target_link_libraries()` to link it to our target, It is important to call it after the target creation (witch is `add_executable` in our case).

`CMakeLists.txt`
```diff
...
+ find_package(SFML COMPONENTS system window graphics network CONFIG REQUIRED)

SET(EXECUTABLE_TARGET_NAME cmake-vcpkg-template-app)

add_executable(${EXECUTABLE_TARGET_NAME}
    main.cpp
)

+ target_link_libraries(${EXECUTABLE_TARGET_NAME}
+     PRIVATE sfml-system sfml-network sfml-graphics sfml-window
+ )
...
```

You must reload your cmake project and reset cache in your IDE or directly with the cmake command to make it work.

__Use SFML in our program to make sure our installation is working :__

For this exemple we will use the [SFML tutorial](https://www.sfml-dev.org/tutorials/2.5/start-linux.php#compiling-a-sfml-program) to make sure our installation is working.
After pasting the exemple code in your `main.cpp` we can now compile our program and run it, you should see a window with a green circle in it and a title "SFML works!".

Congratulations you have successfully installed SFML in your project !
You can now add any other dependencies you want.
