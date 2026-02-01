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
```
cmake -S llvm -B build -G <generator> [options]
```
For a release build with assertions enabled and linking limited to max 1, set up config with this command
```
cmake -S llvm -B build -G Ninja -DCMAKE_BUILD_TYPE=Release  -DLLVM_ENABLE_ASSERTIONS=ON -DLLVM_PARALLEL_LINK_JOBS=1 
```
To build on 14 cores
```
ninja -C build -j 1
```
```
ninja -C build check-llvm -j 10
```
