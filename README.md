Fork from
https://github.com/idiap/fast-transformers

# problems

- conda 环境下找不到nvcc
- setup.py中无法编译cuda依赖

```python
from subprocess import DEVNULL, call
call(["nvcc"], stdout=DEVNULL, stderr=DEVNULL)

error...

如果找到nvcc，应该打印 1
```

# solution

安装pytorch后安装cudatoolkit-dev，注意版本对应前面的cudatoolkit

```bash
conda install -c conda-forge cudatoolkit-dev=10.1  # this takes some time
pip install pytorch-fast-transformers --no-cache-dir  # this also takes some time
```
