# demo-project example with cmake

export build commands and build with ccache:

    cmake .. -DCMAKE_EXPORT_COMPILE_COMMANDS=ON -DCMAKE_CXX_COMPILER_LAUNCHER=ccache

install/uninstall:

    cd build
    make install
    make uninstall

    cmake --build build/ --parallel $(nproc)
    cmake --build build/ --parallel $(nproc) --target install
    cmake --build build/ --parallel $(nproc) --target uninstall
