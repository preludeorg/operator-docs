---
title: "PneumaEX"
slug: "pneumaex"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Aug 08 2022 04:17:18 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Aug 08 2022 04:25:15 GMT+0000 (Coordinated Universal Time)"
---
PneumaEX is a cross-compiled Operator agent which can communicate over all available Operator protocols, including TCP, UDP and HTTP/S. Unlike Pneuma, PneumaEX has a modular plugin system that can dynamically load and execute modules from the command and control server. PneumaEX is only available for Professional and Enterprise users. 

### Downloading PneumaEX

A compiled version of PneumaEX for your operating system can be found in Operator under the agents tab. If you want to build from source, you can download a .zip of the latest build with the following curl command: 

```shell
curl http://0.0.0.0:3391/payloads/pneumaEX/v1.7/pneumaEX.zip > /tmp/pneumaEX.zip
```

### Compile

When you are ready to use PneumaEX in a real environment, you will want to compile it into a binary by running the build.sh script, passing in any string as your unique (public) randomHash string, which ensures each compiled agent gets a different file hash:

```shell
./build.sh JWHQZM9Z4HQOYICDHW4OCJAXPPNHBA
```

On windows you can build with:

```powershell
.\build.ps1 -randomHash "JWHQZM9Z4HQOYICDHW4OCJAXPPNHBA"
```

There is also support for garble builds (Thanks to the amazing work here: <https://github.com/burrowers/garble>):

```shell
GO111MODULE=on go get mvdan.cc/garble
go mod tidy
./garble-build.sh JWHQZM9Z4HQOYICDHW4OCJAXPPNHBA
```

```powershell
GO111MODULE=on go get mvdan.cc/garble
go mod tidy
.\garble-build.ps1 -randomHash "JWHQZM9Z4HQOYICDHW4OCJAXPPNHBA"
```

This will output a file (into the payloads directory) for each supported operating system, which you can copy to any target system and execute normally  
to start the agent. 

> Before you compile, consider changing the AESKey variable inside util/conf/default.json. This value represents  
> the encryption key to encrypt/decrypt communications with Prelude Operator. This key must be 32-characters  
> and must match the encryption key in the Prelude Operator Emulate section. Also consider  
> changing the default address parameters in main.go, so you can start your agent without command-line arguments.

### C-Shared library compilation (DLL, SO, DyLib)

PneumaEX supports cross compilation to 64-bit C-shared libraries depending upon the platform you are building on. When using a C-Shared library,  
you must specifically compile in the parameters you want to configure in the `util/conf/default.json` file (specifically the `address`  
and the `contact` you wish you use).

We currently support:

- **Windows**: `build.ps1` and `garble-build.ps1` builds DLL
- **Darwin**: `build.sh` and `garble-build.sh` builds DLL, Dylib, SO
  - Depends on `x86_64-w64-mingw32-gcc` (Windows) and `x86_64-linux-musl-gcc` (Linux)
- **Linux**: `build.sh` and `garble-build.sh` builds DLL, Dylib, SO
  - Depends on `x86_64-w64-mingw32-gcc` (Windows) and `o64-clang` (Darwin)

To install dependencies on Darwin:

```shell
brew install mingw-w64 FiloSottile/musl-cross/musl-cross
```

To install dependencies on Linux:

```shell
# yum repos for Windows builds
yum install mingw64-gcc

# apt repos for Windows builds
apt-get install mingw64-gcc

# Darwin builds
# Follow the instructions here: https://github.com/tpoechtrager/osxcross
```

You can modify the exported functions by modifying the names of the functions in the `library/library.go` file. Default exported functions:

```go
//export VoidFunc
func VoidFunc()

//export RunAgent
func RunAgent()

//export DllInstall
func DllInstall()

//export DllRegisterServer
func DllRegisterServer()

//export DllUnregisterServer
func DllUnregisterServer()
```
