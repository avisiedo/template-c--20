# My Project

## TODO

- [ ] Update the main title of this project to fit align with your repository.
- [ ] 

## Getting Started

### Install dependencies

**Fedora**

```sh
# General
sudo dnf install -y cmake clang gmock-devel gtest-devel
# If using boost
sudo dnf install -y boost-devel
```

**Ubuntu**

TODO

**Arch Linux**

```raw
sudo pacman -Sy core/make core/clang
```

### Once task

```raw
git submodule init
git submodule update
mkdir build
cd build
cmake ..
make
```

Day to day rules:

```raw
mkdir build; cd build
cmake ..
cmake --build .
cmake --build . --fresh
```

TODO

## Documentation

- [Contributing guideline](docs/CONTRIBUTING.md).
- [Security issue guidelines](docs/SECURITY.md).
- [Triage guidelines](docs/TRIAGE.md).

## Books and references

- [Algorithms in C++](https://www.amazon.com/Algorithms-Parts-1-4-Fundamentals-Structure/dp/0201350882).
- [Effective Modern C++](https://www.amazon.com/Effective-Modern-C-Scott-Meyers/dp/9351109054).
- [CPP Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines).
- [Modern CPP tutorial](https://github.com/changkun/modern-cpp-tutorial).

