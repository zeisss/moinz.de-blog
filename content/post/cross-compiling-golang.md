+++
date = "2013-03-26T00:59:34+02:00"
title = "Cross Compiling Go"
+++

Update: Since Go 1.6 you don't need this anymore. The compiler can always crosscompile.

(I wrote this as a protip on [Coderwall](https://coderwall.com/p/pnfwxg))

Compiling your go code into a binary is pretty simple:

```
$ go install <package>
```

This will build the binary for your current OS and architecture. But compiling binaries for other operating systems and even architectures is also possible. You just need to modify a few environment variables:

* `GOARCH` – the architecture, e.g. amd64, 386 or arm
* `GOOS` – the operating system – linux, darwin or windows

## Building the compiler first …

You can take a look at the output of go env to see what your current configuration looks like. But to actually cross compile, you need to first build the compilers.

With Mac OS / Homebrew, just install go with `--cross-compile-common` or `--cross-compile-all`. See the recipe for details.

If you have installed Go from source, just set the variables and call `./all.bash` in the src folder for each `GOARCH/GOOS` combination you need.

This guide might help if you are totally lost.

## Building your project

Back to our project. Similar to building the compiler you just need to modify the environment variables and call go build as before. Go will now create a subfolder in ./bin/ matching your os/arch combination. Here you will find your cross-compiled binary. Obviously you can also pass in the vars in one line:

```
$ GOARCH=arm GOOS=linux go build helloworld
```

PS: If you want to crosscompile for ARM v5/v6 CPU (e.g. for the raspberry pi), you need to set `GOARM=5` to use different set of operations for floating point math.
