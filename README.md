# Starlet Tests
A repository containing integration and cross-library unit tests for the **Starlet** Engine Ecosystem.    
Tests are written using **Google Test** (gtest) and will focus on multi-module behaviour, engine-level interaction, and system-wide validation.

## Features
This repository is intended for future multi-library test coverage.

<br/>

## Building and Running Tests
This project uses **CMake** and **Google Test**.

### 1. Clone the Repository
```bash
git clone https://github.com/masonlet/starlet-tests.git
cd starlet-tests
```

### 2. Create a Build Directory and Generate Build Files
```bash
mkdir build
cd build
cmake ..
cmake --build .
```

### 3. Run the Tests
```bash
ctest
```
