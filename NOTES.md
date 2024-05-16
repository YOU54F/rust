
./x build --target aarch64-apple-darwin,aarch64-unknown-freebsd --stage 3
rustup toolchain link stage0 build/host/stage0-sysroot 
rustup toolchain link stage1 build/host/stage1
rustup toolchain link stage2 build/host/stage2
rustup toolchain link stage3 build/host/stage3
rustc +stage1 -vV
rustc +stage2 -vV
rustc +stage3 -vV
cd ~/dev/random/pact_cli
cargo +stage3 build --target aarch64-unknown-freebsd --release --config target.aarch64-unknown-freebsd.linker=\'/tmp/loki/bin/aarch64-unknown-freebsd12.3-gcc\'
cargo +stage3 build --target aarch64-unknown-netbsd --release --config target.aarch64-unknown-freebsd.linker=\'/tmp/dakini/bin/aarch64-unknown-netbsd-gcc\'
ls /tmp/dakini/bin/aarch64-unknown-netbsd-*
./x build --target aarch64-apple-darwin,aarch64-unknown-netbsd --stage 3
cargo +stage3 build --target aarch64-unknown-netbsd --release --config target.aarch64-unknown-netbsd.linker=\'/tmp/dakini/bin/aarch64-unknown-netbsd-gcc\'
./x build --target aarch64-apple-darwin,aarch64-unknown-openbsd --stage 3
find /tmp/ -name 'stdalign.h'
CFLAGS="-I/tmp/loki/aarch64-unknown-freebsd12.3/include/" cargo +stage3 build --target aarch64-unknown-openbsd --release --config target.aarch64-unknown-openbsd.linker=\'/tmp/atar/bin/aarch64-unknown-openbsd-gcc\'



```toml
[target.x86_64-unknown-linux-musl]
rustflags = [
    "-L", "/opt/homebrew/Cellar/musl-cross-x86_64/0.9.9_2/libexec/x86_64-linux-musl/lib",
    "-L", "/opt/homebrew/Cellar/musl-cross-x86_64/0.9.9_2/libexec/lib/gcc/x86_64-linux-musl/9.2.0",
    "-L", "/opt/homebrew/opt/libunwind-x86_64-musl/lib",
    "-Z","location-detail=none",
    # "-C","panic=unwind"
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    # "-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
]
linker = "x86_64-linux-musl-gcc"
ar = "x86_64-linux-musl-ar"

[target.x86_64-unknown-linux-gnu]
rustflags = [
    # "-L", "/opt/homebrew/Cellar/musl-cross-x86_64/0.9.9_2/libexec/x86_64-linux-musl/lib",
    # "-L", "/opt/homebrew/Cellar/musl-cross-x86_64/0.9.9_2/libexec/lib/gcc/x86_64-linux-musl/9.2.0",
    # "-L", "/opt/homebrew/opt/libunwind-x86_64-musl/lib",
    "-Z","location-detail=none",
    # "-C","panic=unwind"
    "-C","panic=abort",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",

    # If you want a self contained gnu binary, at the expense of binary size 828K vs 28k
    # "-C", "target-feature=+crt-static",
    # "-C","relocation-model=pie",
    # "-C","relocation-model=static",
]
linker = "x86_64-linux-gnu-gcc"
ar = "x86_64-linux-gnu-ar"
[target.aarch64-unknown-linux-musl]
rustflags = [
    "-L", "/opt/homebrew/Cellar/musl-cross-aarch64/0.9.9_2/libexec/aarch64-linux-musl/lib",
    "-L", "/opt/homebrew/Cellar/musl-cross-aarch64/0.9.9_2/libexec/lib/gcc/aarch64-linux-musl/9.2.0",
    "-L", "/opt/homebrew/opt/libunwind-aarch64-musl/lib",
    "-Z","location-detail=none",
    # "-C","panic=unwind"
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
]
linker = "aarch64-linux-musl-gcc"
ar = "aarch64-linux-musl-ar"
[target.aarch64-unknown-linux-gnu]
rustflags = [
    "-Z","location-detail=none",
    # "-C","panic=unwind"
    "-C","panic=abort",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",


    # If you want a self contained gnu binary, at the expense of binary size 828K vs 28k
    # "-C", "target-feature=+crt-static",
    # "-C","relocation-model=pie",
    # "-C","relocation-model=static",
]
linker = "aarch64-linux-gnu-gcc"
ar = "aarch64-linux-gnu-ar"

[target.arm-unknown-linux-musleabi]
rustflags = [
    "-L", "/opt/homebrew/Cellar/musl-cross-arm/0.9.9_2/libexec/arm-linux-musleabi/lib",
    "-L", "/opt/homebrew/Cellar/musl-cross-arm/0.9.9_2/libexec/lib/gcc/arm-linux-musleabi/9.2.0",
    "-L", "/opt/homebrew/opt/libunwind-arm-hf-musl/lib",
    "-Z","location-detail=none",
    # "-C","panic=unwind"
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]
linker = "arm-linux-musleabi-gcc"
ar = "arm-linux-musleabi-ar"
[target.arm-unknown-linux-gnueabi]
rustflags = [
    # "-C","panic=unwind"
    "-C","panic=abort",
    "-Z","location-detail=none",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",


    # If you want a self contained gnu binary, at the expense of binary size 828K vs 28k
    # "-C", "target-feature=+crt-static",
    # "-C","relocation-model=pie",
    # "-C","relocation-model=static",
    ]
linker = "arm-linux-gnueabi-gcc"
ar = "arm-linux-gnueabi-ar"

[target.arm-unknown-linux-musleabihf]
rustflags = [
    "-L", "/opt/homebrew/Cellar/musl-cross-arm-hf/0.9.9_2/libexec/arm-linux-musleabihf/lib",
    "-L", "/opt/homebrew/Cellar/musl-cross-arm-hf/0.9.9_2/libexec/lib/gcc/arm-linux-musleabihf/9.2.0",
    "-L", "/opt/homebrew/opt/libunwind-arm-hf-musl/lib",
    "-Z","location-detail=none",
    # "-C","panic=unwind"
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
]
linker = "arm-linux-musleabihf-gcc"
ar = "arm-linux-musleabihf-ar"
[target.arm-unknown-linux-gnueabihf]
rustflags = [
    # "-C","panic=unwind"
    "-C","panic=abort",
    "-Z","location-detail=none",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",

    # If you want a self contained gnu binary, at the expense of binary size 828K vs 28k
    # "-C", "target-feature=+crt-static",
    # "-C","relocation-model=pie",
    # "-C","relocation-model=static",
]
linker = "arm-linux-gnueabihf-gcc"
ar = "arm-linux-gnueabihf-ar"


# [target.i386-unknown-linux-musl]
# linker = "i386-linux-musl-gcc"
# ar = "i386-linux-musl-ar"
# [target.i486-unknown-linux-musl]
# linker = "i486-linux-musl-gcc"
# ar = "i486-linux-musl-ar"

[target.i586-unknown-linux-musl]
rustflags = [
    "-L", "/opt/homebrew/Cellar/musl-cross-i586/0.9.9_2/libexec/i586-linux-musl/lib",
    "-L", "/opt/homebrew/Cellar/musl-cross-i586/0.9.9_2/libexec/lib/gcc/i586-linux-musl/9.2.0",
    "-L", "/opt/homebrew/opt/libunwind-i586-musl/lib",
    "-Z","location-detail=none",
    # "-C","panic=unwind"
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]
linker = "i586-linux-musl-gcc"
ar = "i586-linux-musl-ar"
[target.i686-unknown-linux-musl]
rustflags = [
    "-L", "/opt/homebrew/Cellar/musl-cross-i686/0.9.9_2/libexec/i686-linux-musl/lib",
    "-L", "/opt/homebrew/Cellar/musl-cross-i686/0.9.9_2/libexec/lib/gcc/i686-linux-musl/9.2.0",
    "-L", "/opt/homebrew/opt/libunwind-i686-musl/lib",
    "-Z","location-detail=none",
    # "-C","panic=unwind"
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]
linker = "i686-linux-musl-gcc"
ar = "i686-linux-musl-ar"
[target.i686-unknown-linux-gnu]
rustflags = [
    # "-C","panic=unwind"
    "-C","panic=abort",
    "-Z","location-detail=none",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",

    # If you want a self contained gnu binary, at the expense of binary size 828K vs 28k
    # "-C", "target-feature=+crt-static",
    # "-C","relocation-model=pie",
    # "-C","relocation-model=static",
    ]
linker = "i686-linux-gnu-gcc"
ar = "i686-linux-gnu-ar"



# linker = "powerpc-sf-linux-musl-gcc"
# ar = "powerpc-sf-linux-musl-ar"
# [target.powerpc-unknown-linux-musl]
# linker = "powerpc-linux-musl-gcc"
# ar = "powerpc-linux-musl-ar"
# [target.powerpc64-unknown-linux-musl]
# linker = "powerpc64-linux-musl-gcc"
# ar = "powerpc64-linux-musl-ar"

[target.powerpc64le-unknown-linux-musl]
rustflags = [
    "-L", "/opt/homebrew/Cellar/musl-cross-powerpc64le/0.9.9_2/libexec/powerpc64le-linux-musl/lib",
    "-L", "/opt/homebrew/Cellar/musl-cross-powerpc64le/0.9.9_2/libexec/lib/gcc/powerpc64le-linux-musl/9.2.0",
    "-L", "/opt/homebrew/opt/libunwind-powerpc64le-musl/lib",
    "-Z","location-detail=none",
    # "-C","panic=unwind"
    "-C","panic=abort",
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]
linker = "powerpc64le-linux-musl-gcc"
ar = "powerpc64le-linux-musl-ar"
# [target.powerpc-sf-unknown-linux-mu
[target.s390x-unknown-linux-musl]
rustflags = [
    "-L", "/opt/homebrew/Cellar/musl-cross-s390x/0.9.9_2/libexec/s390x-linux-musl/lib",
    "-L", "/opt/homebrew/Cellar/musl-cross-s390x/0.9.9_2/libexec/lib/gcc/s390x-linux-musl/9.2.0",
    "-L", "/opt/homebrew/opt/libunwind-s390x-musl/lib",
    "-Z","location-detail=none",
    # "-C","panic=unwind",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]
linker = "s390x-linux-musl-gcc"
ar = "s390x-linux-musl-ar"

[target.riscv64gc-unknown-linux-musl]
rustflags = [
    "-L", "/opt/homebrew/Cellar/musl-cross-riscv64/0.9.9_2/libexec/riscv64-linux-musl/lib",
    "-L", "/opt/homebrew/Cellar/musl-cross-riscv64/0.9.9_2/libexec/lib/gcc/riscv64-linux-musl/9.2.0",
    "-L", "/opt/homebrew/opt/libunwind-riscv64-musl/lib",
    # "-C","panic=unwind",
    "-C","panic=abort",
    "-C", "target-feature=+crt-static",
    "-Z","location-detail=none",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]
linker = "riscv64-linux-musl-gcc"
ar = "riscv64-linux-musl-ar"


# https://github.com/rust-lang/rust/blob/1cec373f65eb76e8e4b4d1847213cf3ec6c292b6/compiler/rustc_target/src/spec/base/apple/mod.rs#L273
# rustc --print deployment-target --target aarch64-apple-darwin
# deployment_target=11.0
[target.aarch64-apple-darwin]
rustflags = [
    # "-C","panic=unwind",
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-Z","location-detail=none",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]

# rustc --print deployment-target --target x86_64-apple-darwin
# deployment_target=10.12
[target.x86_64-apple-darwin]
rustflags = [
    "-Z","location-detail=none",
    # "-C","panic=unwind",
    "-C","panic=abort",
    "-C", "target-feature=+crt-static",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]
[target.x86_64-pc-windows-gnu]
rustflags = [
    # "-C","panic=unwind",
    "-C","panic=abort",
    "-Z","location-detail=none",
    "-C", "target-feature=+crt-static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]
[target.i686-pc-windows-gnu]
rustflags = [
    # "-C","panic=unwind",
    "-C","panic=abort",
    "-Z","location-detail=none",
    "-C", "target-feature=+crt-static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]
[target.aarch64-pc-windows-msvc]
rustflags = [
    # "-C","panic=unwind",
    "-C","panic=abort",
    "-Z","location-detail=none",
    "-C", "target-feature=+crt-static",
    "-C","strip=symbols",
    #"-C","lto=true",
    "-C","linker-flavor=lld-link",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
    ]
# linker = "aarch64-pc-windows-msvc-gcc"
[target.aarch64-unknown-freebsd]
rustflags = [
    "-L", "/tmp/loki/aarch64-unknown-freebsd12.3/lib/",
    "-L", "/tmp/loki/lib/",
    "-L", "/tmp/loki/libexec/",
    # "-Z","location-detail=none",
    # "-C","panic=unwind",
    # "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    "-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
]
linker = "/tmp/loki/bin/aarch64-unknown-freebsd12.3-gcc"
ar = "/tmp/loki/bin/aarch64-unknown-freebsd12.3-ar"
[target.x86_64-unknown-freebsd]
rustflags = [
    "-L", "/tmp/loki/x86_64-unknown-freebsd12.3/lib/",
    "-L", "/tmp/loki/lib/",
    "-L", "/tmp/loki/libexec/",
    # "-Z","location-detail=none",
    # "-C","panic=unwind",
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    "-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
]
linker = "/tmp/loki/bin/x86_64-unknown-freebsd12.3-gcc"
ar = "/tmp/loki/bin/x86_64-unknown-freebsd12.3-ar"
[target.x86_64-unknown-openbsd]
rustflags = [
    "-L", "/tmp/atar/x86_64-unknown-openbsd/lib/",
    "-L", "/tmp/atar/x86_64-unknown-openbsd/bin/",
    # "-Z","location-detail=none",
    # "-C","panic=unwind",
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    "-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
]
linker = "/tmp/atar/bin/x86_64-unknown-openbsd-gcc"
ar = "/tmp/atar/bin/x86_64-unknown-openbsd-ar"
[target.aarch64-unknown-openbsd]
rustflags = [
    "-L", "/tmp/atar/aarch64-unknown-openbsd/lib/",
    "-L", "/tmp/atar/aarch64-unknown-openbsd/bin/",
    # "-Z","location-detail=none",
    # "-C","panic=unwind",
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    "-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
]
linker = "/tmp/atar/bin/aarch64-unknown-openbsd-gcc"
ar = "/tmp/atar/bin/aarch64-unknown-openbsd-ar"
[target.x86_64-unknown-netbsd]
rustflags = [
    "-L", "/tmp/dakini/x86_64-unknown-netbsd/lib/",
    "-L", "/tmp/dakini/x86_64-unknown-netbsd/bin/",
    # "-Z","location-detail=none",
    # "-C","panic=unwind",
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    "-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
]

linker = "/tmp/dakini/bin/x86_64-unknown-netbsd-gcc"
ar = "/tmp/dakini/bin/x86_64-unknown-netbsd-ar"

[target.aarch64-unknown-netbsd]
rustflags = [
    "-L", "/tmp/dakini/aarch64-unknown-netbsd/lib/",
    "-L", "/tmp/dakini/aarch64-unknown-netbsd/bin/",
    # "-Z","location-detail=none",
    # "-C","panic=unwind",
    "-C", "target-feature=+crt-static",
    "-C","panic=abort",
    "-C","relocation-model=pie",
    "-C","relocation-model=static",
    "-C","strip=symbols",
    "-C","lto=true",
    "-C","opt-level=z",
    "-C","codegen-units=1",
    "-C","embed-bitcode=true",
]
linker = "/tmp/dakini/bin/aarch64-unknown-netbsd-gcc"
ar = "/tmp/dakini/bin/aarch64-unknown-netbsd-ar"

    # "arm-unknown-linux-musleabihf", # undefined symbol: __aeabi_unwind_cpp_pr0 etc, same for below, needs stubbing, or fixing in libunwind cross builds
    # "arm-unknown-linux-musleabi",
    # "i586-unknown-linux-musl",
    # "powerpc64le-unknown-linux-musl",

    # BSD's

[build]
target = [
    "aarch64-apple-darwin",
    "x86_64-apple-darwin",
    "x86_64-unknown-linux-gnu", 
    "x86_64-unknown-linux-musl", 
    "aarch64-unknown-linux-gnu",
    "aarch64-unknown-linux-musl",
    "arm-unknown-linux-gnueabihf",
    "arm-unknown-linux-gnueabi",
    "i686-unknown-linux-musl",
    "i686-unknown-linux-gnu",
    "s390x-unknown-linux-musl",
    "riscv64gc-unknown-linux-musl",
    "x86_64-unknown-freebsd",
    "x86_64-unknown-openbsd",
    "x86_64-unknown-netbsd",
    "aarch64-unknown-freebsd",
    "aarch64-unknown-openbsd",
    "aarch64-unknown-netbsd",
    "i586-unknown-linux-musl",
    # "arm-unknown-linux-musleabihf", # undefined symbol: __aeabi_unwind_cpp_pr0 etc, same for below, needs stubbing, or fixing in libunwind cross builds
    # "arm-unknown-linux-musleabi",
    # "powerpc64le-unknown-linux-musl",
    ]

    # "armv6-unknown-freebsd",
    # "armv7-unknown-freebsd",
    # "powerpc-unknown-freebsd",
    # "powerpc64-unknown-freebsd",
    # "powerpc64le-unknown-freebsd",
    # "riscv64gc-unknown-freebsd",
    # "aarch64_be-unknown-netbsd",
    # "armv6-unknown-netbsd-eabihf",
    # "armv7-unknown-netbsd-eabihf",
    # "i586-unknown-netbsd",
    # "i686-unknown-netbsd",
    # "mipsel-unknown-netbsd",
    # "powerpc-unknown-netbsd",
    # "riscv64gc-unknown-netbsd",
    # "sparc64-unknown-netbsd",
    # "i686-unknown-openbsd",
    # "powerpc-unknown-openbsd",
    # "powerpc64-unknown-openbsd",
    # "riscv64gc-unknown-openbsd",
    # "sparc64-unknown-openbsd",
# [unstable]
# build-std = ["std", "panic_abort", "core", "alloc"]
# build-std-features = ["panic_immediate_abort"]


# cargo +nightly build --release -Zbuild-std=std,panic_abort -Z build-std-features=panic_immediate_abort
# cargo +nightly xwin build --release -Zbuild-std=std,panic_abort -Z build-std-features=panic_immediate_abort --target x86_64-pc-windows-gnu
# cargo +nightly xwin build --release -Zbuild-std=std,panic_abort -Z build-std-features=panic_immediate_abort --target i686-pc-windows-gnu
# cargo +nightly xwin build --release -Zbuild-std=std,panic_abort -Z build-std-features=panic_immediate_abort --target aarch64-pc-windows-msvc

# target = [
    # "x86_64-pc-windows-gnu",
    # "i686-pc-windows-gnu",
    # "aarch64-pc-windows-msvc"
    # ]

```