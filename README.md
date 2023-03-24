# Cmake & vcpkg template

This is a template repository made to quick setup a project using cmake & vcpkg

I usualy use Clion as IDE so this repository have a basic .idea configuration

## Setting up dependencies

```bash
git submodule update --init --recursive
```

## Adding dependencies

You can add any vcpkg dependencies by editing vcpkg.json

__Exemple with SFML__ :

`vcpkg.json`
```json
{
  "name": "cmake-vcpkg-template",
  "version": "0.1.0",
  "builtin-baseline": "6ca56aeb457f033d344a7106cb3f9f1abf8f4e98",
  "dependencies": [
    {
        "name" : "SFML",
        "version" : "2.5.1"
    }
  ],
  "overrides": [
    {
      "name": "freetype",
      "version" : "2.10.0"
    }
  ]
}
```

In this exemple i override the `freetype` version to `2.10.0` (who is a font reading library) because sometime it cause an issues on windows.

For further informations you check the [microsoft documentation about vcpkg.json](https://learn.microsoft.com/en-us/vcpkg/reference/vcpkg-json)

## Installing dependencies

Bootstrap vcpkg :

Windows
```bash
`.\vcpkg\bootstrap-vcpkg.bat`
```

Unix
```bash
`.\vcpkg\bootstrap-vcpkg.sh`
```

Install depencies :

```bash
`.\vcpkg\vcpkg.exe install --triplet x64-windows`
```