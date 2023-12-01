# go命令
Go（Golang）提供了多种构建参数，它们可以在使用go build、go install等命令时通过命令行传递。这些参数允许开发者控制编译过程，优化生成的可执行文件，甚至指定特定的编译行为。下面是一些常用的Go构建参数及其含义：

# 常用构建参数
1. -o
含义：指定输出的可执行文件或其他对象文件的名称。
示例：go build -o myapp。这会将编译后的程序输出为myapp。
2. -i
含义：在Go 1.10之前，此参数用于安装依赖包的编译文件到pkg目录。在Go 1.10及之后的版本中，由于构建缓存的引入，这个参数的效果变得微乎其微。
3. -v
含义：打印出正在编译的包名。
示例：go build -v。
4. -race
含义：启用数据竞争检测。在编译时开启对数据竞争的检测，主要用于开发阶段查找并发bug。
示例：go build -race。
5. -work
含义：打印编译时使用的临时工作目录的路径，并在编译完成后保留该目录。
示例：go build -work。
6. -x
含义：打印出执行的详细命令，对于调试构建过程非常有用。
示例：go build -x。
7. -gcflags
含义：传递给编译器的标志。可以用来调整优化级别或打开某些诊断特性。
示例：go build -gcflags="-N -l"。-N 禁用优化，-l 禁用内联。
8. -ldflags
含义：传递给链接器的标志。常用于设置编译时的变量，比如版本号，或者控制生成的二进制文件的性质，如去掉调试信息等。
示例：go build -ldflags="-X main.version=1.0.0"。
9. -tags
含义：指定构建标签。这允许在编译时启用或禁用代码中的特定部分。
示例：go build -tags="prod"。
10. -mod
含义：模块下载模式。例如，可以设置为readonly，表示在构建时不会自动修改go.mod文件。
示例：go build -mod=readonly。
11. -trimpath
含义：移除二进制文件中的所有文件路径信息，常用于构建时保护源代码路径的隐私或出于安全考虑。
示例：go build -trimpath。
这些是Go编译和安装时比较常用的一些参数。Go的构建系统非常灵活，通过这些参数，开发者可以对构建过程进行详细的控制。不过，需要注意的是，并不是所有参数在所有情况下都适用，有些参数可能只在特定的Go版本中有效或者在特定的上下文中才有意义。

## build
```txt
$ go help build
usage: go build [-o output] [build flags] [packages]

Build compiles the packages named by the import paths,
along with their dependencies, but it does not install the results.

If the arguments to build are a list of .go files from a single directory,
build treats them as a list of source files specifying a single package.

When compiling packages, build ignores files that end in '_test.go'.

When compiling a single main package, build writes
the resulting executable to an output file named after
the first source file ('go build ed.go rx.go' writes 'ed' or 'ed.exe')
or the source code directory ('go build unix/sam' writes 'sam' or 'sam.exe').
The '.exe' suffix is added when writing a Windows executable.

When compiling multiple packages or a single non-main package,
build compiles the packages but discards the resulting object,
serving only as a check that the packages can be built.

The -o flag forces build to write the resulting executable or object
to the named output file or directory, instead of the default behavior described
in the last two paragraphs. If the named output is an existing directory or
ends with a slash or backslash, then any resulting executables
will be written to that directory.

The -i flag installs the packages that are dependencies of the target.
The -i flag is deprecated. Compiled packages are cached automatically.

The build flags are shared by the build, clean, get, install, list, run,
and test commands:

        -a
                force rebuilding of packages that are already up-to-date.
        -n
                print the commands but do not run them.
        -p n
                the number of programs, such as build commands or
                test binaries, that can be run in parallel.
                The default is GOMAXPROCS, normally the number of CPUs available.
        -race
                enable data race detection.
                Supported only on linux/amd64, freebsd/amd64, darwin/amd64, darwin/arm64, windows/amd64,
                linux/ppc64le and linux/arm64 (only for 48-bit VMA).
        -msan
                enable interoperation with memory sanitizer.
                Supported only on linux/amd64, linux/arm64
                and only with Clang/LLVM as the host C compiler.
                On linux/arm64, pie build mode will be used.
        -asan
                enable interoperation with address sanitizer.
                Supported only on linux/arm64, linux/amd64.
                Supported only on linux/amd64 or linux/arm64 and only with GCC 7 and higher
                or Clang/LLVM 9 and higher.
        -v
                print the names of packages as they are compiled.
        -work
                print the name of the temporary work directory and
                do not delete it when exiting.
        -x
                print the commands.

        -asmflags '[pattern=]arg list'
                arguments to pass on each go tool asm invocation.
        -buildmode mode
                build mode to use. See 'go help buildmode' for more.
        -buildvcs
                Whether to stamp binaries with version control information
                ("true", "false", or "auto"). By default ("auto"), version control
                information is stamped into a binary if the main package, the main module
                containing it, and the current directory are all in the same repository.
                Use -buildvcs=false to always omit version control information, or
                -buildvcs=true to error out if version control information is available but
                cannot be included due to a missing tool or ambiguous directory structure.
        -compiler name
                name of compiler to use, as in runtime.Compiler (gccgo or gc).
        -gccgoflags '[pattern=]arg list'
                arguments to pass on each gccgo compiler/linker invocation.
        -gcflags '[pattern=]arg list'
                arguments to pass on each go tool compile invocation.
        -installsuffix suffix
                a suffix to use in the name of the package installation directory,
                in order to keep output separate from default builds.
                If using the -race flag, the install suffix is automatically set to race
                or, if set explicitly, has _race appended to it. Likewise for the -msan
                and -asan flags. Using a -buildmode option that requires non-default compile
                flags has a similar effect.
        -ldflags '[pattern=]arg list'
                arguments to pass on each go tool link invocation.
        -linkshared
                build code that will be linked against shared libraries previously
                created with -buildmode=shared.
        -mod mode
                module download mode to use: readonly, vendor, or mod.
                By default, if a vendor directory is present and the go version in go.mod
                is 1.14 or higher, the go command acts as if -mod=vendor were set.
                Otherwise, the go command acts as if -mod=readonly were set.
                See https://golang.org/ref/mod#build-commands for details.
        -modcacherw
                leave newly-created directories in the module cache read-write
                instead of making them read-only.
        -modfile file
                in module aware mode, read (and possibly write) an alternate go.mod
                file instead of the one in the module root directory. A file named
                "go.mod" must still be present in order to determine the module root
                directory, but it is not accessed. When -modfile is specified, an
                alternate go.sum file is also used: its path is derived from the
                -modfile flag by trimming the ".mod" extension and appending ".sum".
        -overlay file
                read a JSON config file that provides an overlay for build operations.
                The file is a JSON struct with a single field, named 'Replace', that
                maps each disk file path (a string) to its backing file path, so that
                a build will run as if the disk file path exists with the contents
                given by the backing file paths, or as if the disk file path does not
                exist if its backing file path is empty. Support for the -overlay flag
                has some limitations: importantly, cgo files included from outside the
                include path must be in the same directory as the Go package they are
                included from, and overlays will not appear when binaries and tests are
                run through go run and go test respectively.
        -pkgdir dir
                install and load all packages from dir instead of the usual locations.
                For example, when building with a non-standard configuration,
                use -pkgdir to keep generated packages in a separate location.
        -tags tag,list
                a comma-separated list of additional build tags to consider satisfied
                during the build. For more information about build tags, see
                'go help buildconstraint'. (Earlier versions of Go used a
                space-separated list, and that form is deprecated but still recognized.)
        -trimpath
                remove all file system paths from the resulting executable.
                Instead of absolute file system paths, the recorded file names
                will begin either a module path@version (when using modules),
                or a plain import path (when using the standard library, or GOPATH).
        -toolexec 'cmd args'
                a program to use to invoke toolchain programs like vet and asm.
                For example, instead of running asm, the go command will run
                'cmd args /path/to/asm <arguments for asm>'.
                The TOOLEXEC_IMPORTPATH environment variable will be set,
                matching 'go list -f {{.ImportPath}}' for the package being built.

The -asmflags, -gccgoflags, -gcflags, and -ldflags flags accept a
space-separated list of arguments to pass to an underlying tool
during the build. To embed spaces in an element in the list, surround
it with either single or double quotes. The argument list may be
preceded by a package pattern and an equal sign, which restricts
the use of that argument list to the building of packages matching
that pattern (see 'go help packages' for a description of package
patterns). Without a pattern, the argument list applies only to the
packages named on the command line. The flags may be repeated
with different patterns in order to specify different arguments for
different sets of packages. If a package matches patterns given in
multiple flags, the latest match on the command line wins.
For example, 'go build -gcflags=-S fmt' prints the disassembly
only for package fmt, while 'go build -gcflags=all=-S fmt'
prints the disassembly for fmt and all its dependencies.

For more about specifying packages, see 'go help packages'.
For more about where packages and binaries are installed,
run 'go help gopath'.
For more about calling between Go and C/C++, run 'go help c'.

Note: Build adheres to certain conventions such as those described
by 'go help gopath'. Not all projects can follow these conventions,
however. Installations that have their own conventions or that use
a separate software build system may choose to use lower-level
invocations such as 'go tool compile' and 'go tool link' to avoid
some of the overheads and design decisions of the build tool.

See also: go install, go get, go clean.
```