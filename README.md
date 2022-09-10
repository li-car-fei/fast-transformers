Fork from
https://github.com/idiap/fast-transformers

# problems

- conda 环境下找不到nvcc
- setup.py中无法编译cuda依赖
- pytorch版本过高在编译fast-transformers时会有问题

先查看当前路径下能否找到nvcc依赖：
```python
from subprocess import DEVNULL, call
call(["nvcc"], stdout=DEVNULL, stderr=DEVNULL)

error...

如果找到nvcc，应该打印 1

```
也可以直接`nvcc --version`查看信息

# solution

先安装pytorch，再安装cudatoolkit-dev，注意对应linux机器的cudatoolkit版本

```bash
conda search -c conda-forge cudatoolkit-dev          # 先查看对应的版本
conda install -c conda-forge cudatoolkit-dev=11.2    # 使得nvcc可以被找到
```

```bash
linux 下：
pip install pytorch-fast-transformers --user --no-cache-dir  # 重新编译，不依赖缓存

windows下：
pip install git+https://github.com/maxgraf96/fast-transformers --user --no-cache-dir # windows改动

或使用本库：
pip install git+https://github.com/li-car-fei/fast-transformers --user --no-cache-dir # 编译过程改动
```

如果setup过程中出现以下问题：
```bash
subprocess.CalledProcessError: Command '['ninja', '-v']' returned non-zero exit status 1.
```
参看以下：https://blog.csdn.net/qq_41452267/article/details/124087590
