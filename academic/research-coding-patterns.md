# Patterns for Research Coding

This article is always a work in progress and will be updated periodically.

## "Reproducability Matters (A LOT)"

- your code is original work of creativity
- promotes human knowledge
- trust your code
- academic integrity

## "Always Use Version Control"

**When to commit?**

- Commit at end of a working day.**(MUST)**
- Commit at major feature updates.**(MUST)**
- Learn to use branching.(Optional, as the nature of scientific computing)

**Tips**

- Use straight-forward and meaningful commit messages, like `Updated model selection`, `Added parameter grid search`, not `Major updates`, `Minor modifications`.
- Avoid too-frequent commit, which will distract the clean timeline.

## Practice Basic Project Management

Keep raw copy of important data before modifying.

```bash

```

Make a folder organized by projects.

```
Projects
|-- Project_Name_1
|-- Project_Name_2
`-- Project_Name_3
```

## "A Well-Structured Project Saves Time"

> setup directories hierachies like it's software architecture

### Understand the files

- `README.md`
- `LICENSE`
- `.gitignore`
- `some_package_manager.json`

### Seperate code from data

You definitely would not like your directory to structure like this.

```
Project_Name
|-- code1.py
|-- important_fig.png
|-- code2.py
|-- notes.md
|-- .gitignore
|-- data_201804.npy
|-- LICENSE
`-- README
```

A ideal directory structure would be

```
Project_Name
|-- Codes
|-- Datasets
`-- Figures

# With code files and supporting documents added

Project_Name
|-- Codes
|   |-- code1.py
|   `-- code2.py
|-- Datasets
|   `-- data_01.npy
|-- Figures
|   `-- fig_01.png
|-- .gitignore
|-- LICENSE
`-- README.md
```

Alternatively, you can also **seperate files by input/output**

```
Project_Name
|-- Input
|-- Output
`-- Working
```

**Seperate demos, tests and temp files**

If your project involves a lot of fancy presentation, and ready-to-go trials, you should seperate them like version releases. Demos and tests should be based on fully-functional code from main repository (better to note the version in front matter), simply copied to fine-tune the parameters and do additional visualizations/outputs jobs. Remember to keep a note on which demo/test does what for future reference.

Note that the `Tests` here does not refer to software tests, but more like non-automated function trials.

```
Project_Name
|-- Demos
|   |-- Demo_1
|   `-- Demo_2
|-- Tests
|   `-- test_1.py
`-- Temp
    `-- snippet_1.py
```

### Setup logging

For many, debugging may be a especially painful process.

See [Logging Recipe](https://liuzhenqi77.gitbooks.io/python-notes/content/practice/logging-recipe.html) for detailed configurations of Python's logging module.

### Setup (auto-)saving

**Setup checkpoints**

**Record trial options, inputs and outputs**

### Automate workflow

## "Coding Practical Guidelines"

**Refactor at any point**

**Be easy to iterate (sweep options)**

Suppose we are doing a task involving multiple parameters with a expansion of range. The following function provides no options for iteration. More oftenly, we need a explicit interface for iterate through the parameters. Like, we wanted to plot a surface in 3 dimentions, which involves generating a 2d array.

```python
# hard to iterate
import math
def run():
    x = 2
    y = 2
    # do something with x and y
    z = math.sqrt(x**2 + y**2)
    print(f'{x:} {y:} -> {z:}')
```

```python
# better (support default parameter)
def run(x=2, y=2):
    # do something with x and y
    print(f'{param_1:} -> {param_2:}')

# use list to provide parameters for iteration
param_1s = [1, 2, 3, 4, 5]
param_2s = ['adam', 'joe', 'bob']
# nested iteration
for param_1 in param_1s:
    for param_2 in param_2s:
        run(param_1, param_2)
# or (for those who hate multi-level indentation)
from itertools import product
for param_1, param_2 in product(param_1s, param_2s)
    run(param_1, param_2)
```

A more advanced paradigm (Modified from [Ref 3](#references))

### Run only a subset of your code

### Seperate computation from drawing

## "Snippets of Your Utility Code"

## "Keep Detailed Experiment Notes (Journals)"

```
##########
#  0326  #
##########
===
状态：完成
任务：作 levina 模型的 powerlaw 图
意义：验证 SOC 条件下 powerlaw 结果很好，而另外两个模型没有如此特性(需要细调)
数据：figs/levina_1_powerlaw_*
代码：levina_1.py
备注：~=1.5
===
===
状态：完成
任务：作 izhi 模型关于参数 I 系数的 DFA alpha 曲面图
意义：用于分析 izhi 模型如何选择 I 数值做任务
数据：outputs/izhi_1_I_*, figs/izhi_1_var_Ie_Ii_*
代码：izhi_1_r1.py
备注：
1.  I_e_coeff 应取 6->7.5->7->8.5
2.  I_i_coeff 应取 1->4
===
===
状态：失败
任务：尝试 izhi 模型做任务(如果 DFA 结果好)
意义：
数据：
代码：izhi_2.py
备注：
1.  修改 lasting_time 和 washout，有两处
2.  尝试不同长度输入，输入的不同持续时间
3.  尝试更改电流强度系数
4.  目前分类结果 2 bit 最好达到 0.5，但明显受最后一个发放的影响
5.  最好结果分类效果不显著
===
```

When doing a specific task, the output data and figures can be in rapid iteration and the situation quickly becomes overwhelming.

```python
import time
time_str = time.strftime("%Y%m%d_%H%M%S")
print(f'file_name_{time_str:}')
```

```
Figs
|-- code_1_20180412_041115.png
|-- code_1_20180412_041546.png
`-- code_1_20180412_051235.png
```

Keep a hand-written or text file to track different settings/groups.

## "Spend Time Learning (NEW) Tools"

### IDEs and editors

**Use IDEs,**

- Visual Studio
- Jetbrains Pycharm/IDEA

**Or modern editors,**

- Visual Studio Code
- Atom
- Sublime Text

**With great coding fonts,**

- [FiraCode](https://github.com/tonsky/FiraCode) **(Highly recommended)**
- [ProgrammingFonts](https://github.com/ProgrammingFonts/ProgrammingFonts)
- [nerd-fonts](https://github.com/ryanoasis/nerd-fonts)

**And must-have plugins.**

Plugins that every editor should have

### Plugins

### Utilities

### Libraries

## References

1. [The PhD starter kit](https://blog.gsaneuro.com/2016/01/20/the-phd-starter-kit/)
2. [Principles of Research Code](http://www.theexclusive.org/2012/08/principles-of-research-code.html)
3. [Patterns for Research in Machine Learning](arkitus.com/patterns-for-research-in-machine-learning/)
4. [Directory Tree Generator](http://jsfiddle.net/WjAk9/7/embedded/result/)