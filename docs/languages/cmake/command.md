# Command

## configure

```bash
cmake ..

cmake .. -DUSE_MATH=ON

cmake -S . -B build

cmake -B build -G "Visual Studio 16 2019" -A [Win32|x64] -DCMAKE_GENERATOR_TOOLSET=[v140| v141]

cmake -B build -G "Visual Studio 15 2017" -DCMAKE_GENERATOR_TOOLSET=[v140|v141]

cmake -B build -G "Visual Studio 15 2017 Win64" -DCMAKE_GENERATOR_TOOLSET=[v140|v141]

cmake -B build -G "Visual Studio 15 2017" -DCMAKE_GENERATOR_TOOLSET=[v140|v141] -DCPACK_SYSTEM_NAME=win32-debug
```

## generate

```bash
cmake --build .

cmake --build . --config [Debug|Release]

cmake --build . --target ${PROJECT_NAME}

cmake --build . --config [Debug|Release] --target ${TARGET}
```

## install

```bash
cmake --install . --prefix ./install

cmake --install . --prefix ./install --config Debug
```

## test

```bash
ctest -C Debug

ctest -C Debug -N

ctest -C Debug -V

ctest -C Debug -VV

ctest -VV -C $config_type --test-dir ./$config_type
```

## cpack

```bash
cpack

cpack -G [NSIS | 7Z | ZIP | TGZ]

cpack -G NSIS --config CPackConfig.cmake

cpack -G NSIS -C Debug --config CPackConfig.cmake

cpack -G NSIS -C Release --config CPackConfig.cmake

cpack -G ZIP -B ./$config_type -C $config_type --config ./$config_type/CPackConfig.cmake
```
