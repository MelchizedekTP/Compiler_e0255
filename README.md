# Compiler (E0 255)

## Building LLVM

Download LLVM from git [here](https://github.com/llvm/llvm-project)
To save storage and speed up the checkout time, you may want to do a shallow clone. For example, to get the latest revision of the LLVM project, use
```
git clone --depth 1 https://github.com/llvm/llvm-project.git
```
You are likely not interested in the user branches in the repo (used for stacked pull requests and reverts), you can filter them from your git fetch (or git pull) with this configuration:
```
cd llvm-project
```
```
git config --add remote.origin.fetch '^refs/heads/users/*'
git config --add remote.origin.fetch '^refs/heads/revert-*'
```
To remove the ones already cluttering your local remote-tracking list, run:
```
git fetch origin --prune
```
To build LLVM

Install dependencies 

```
sudo apt update
sudo apt install build-essential ninja-build cmake

```
```
cmake -S llvm -B build -G <generator> [options]
```
For a release build with assertions enabled and linking limited to max 1, set up config with this command
```
cmake -S llvm -B build -G Ninja -DCMAKE_BUILD_TYPE=Release  -DLLVM_ENABLE_ASSERTIONS=ON -DLLVM_PARALLEL_LINK_JOBS=1 
```
To build on 1 cores
```
ninja -C build -j 1
```
To run test
```
ninja -C build check-llvm -j 10
```
As it runs, you will see a progress bar and a summary of results:

- PASS: The test behaved as expected.

- XFAIL (Expected Failure): The test is known to fail (usually a known bug), so it's considered a "pass" for the test runner.

- UNSUPPORTED: The test was skipped (e.g., you’re building on Linux but the test is for Windows-only features).

- FAIL: This is the one to watch. It means the tool's output didn't match the expected "Check" lines.
