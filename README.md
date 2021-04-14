# Rust SGX - Template project
==================================

### This is a template project to start developing with the Teaenclave Rust SGX SDK (https://github.com/apache/incubator-teaclave-sgx-sdk/) easily.

You will find in its template:
- Makefiles to build your project easily, and link the ```SGX EDL C``` generated files to your Rust SGX projects
- The file ```buildenv.mk``` that contains compilation rules when building enclave. No need to specify anymore where this file is located.
- The file ```build.rs``` already configured to build the app/host part properly.
- The file rust-toolchain, so we can force the use of one specific toolchain (```nightly-2020-10-25``` in this case)
- ```Cargo/Xargo.toml``` files to set up your project easily. All the dependencies you might need has been added.

You can find those files in this template: 

```
|-- app/
|   |-- src/
|   |-- Cargo.toml
|   |-- Makefile
|   |-- build.rs
|   +-- rust-toolchain
|-- enclave/
|   |-- src/
|   |-- Cargo.toml
|   |-- Enclave.config.xml
|   |-- Enclave.edl
|   |-- Enclave.lds
|   |-- Makefile
|   |-- Xargo.toml
|   +-- rust-toolchain
|-- Makefile
+-- buildenv.mk
```

## Setting up your project

You need to follow a few steps to use this template properly:
- Add your ```.rs``` files to the ```src/``` folders (```lib.rs``` / your enclave source code goes in ```enclave/src```, your host/app source code goes in ```app/src```)
- Add your own ```Enclave.edl``` file, or modify the one joined in the project.
- Change the ```Cargo.toml (or/and Xargo.toml if you want to use Xargo)``` files depending of your needs. 
    - Be careful if you want to change the library name on the ```Cargo.toml``` file (enclave part), you will need to reflect this change on the enclave ```Makefile```, more specifically on the ```ENCLAVE_CARGO_LIB``` variable.
    - If you need to change the app/host name, please make sure to edit the host ```Makefile```, and change the variable ```APP_U```.

## Build your project

### Before starting the building process, please make sure you downloaded the Rust SGX SDK repository, we're going to need the EDL and headers files joined in the SDK.

Once you downloaded the Rust SGX SDK, you have multiple ways to start the building process: 
- Run this command: ```CUSTOM_EDL_PATH=sdk_location/edl CUSTOM_COMMON_PATH=sdk_location/common make``` (replace sdk_location by the actual SDK location)
- You can also run the command export (```export CUSTOM_EDL_PATH=sdk_location/edl```), and specify the variables before calling make. It is adviced to add this command on your ```.bashrc``` file (if you use bash), or your favorite shell configuration file.

### By default, your project will be compiled in hardware mode. If you wish to compile your project in software/simulation mode, you will need to specify it, either by adding ```SGX_MODE=SW``` before make, or by setting the SGX_MODE variable environment to SW.

### Cargo is used by default when compiling, but you can also use Xargo either by adding ```XARGO_SGX=1``` before make, or by setting the XARGO_SGX variable environment to 1. You will also need to specify Xargo library path with XARGO_PATH.
