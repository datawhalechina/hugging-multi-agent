---
comments: true
---

# 1. 获取MetaGPT

- 使用pip获取MetaGPT  

metagpt可以直接用 pip 来获取至本地环境中，这样我们就可以在像使用任何python包一样导入MetaGPT
通过在终端内运行下面的代码来获取稳定版metagpt

```bash
pip install metagpt
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple metagpt==0.6.6（推荐）
```

通过在终端内运行下面的代码来获取最新版metagpt来体验最新功能

```bash
pip install git+https://github.com/geekan/MetaGPT
```

- 通过github仓库获取MetaGPT

通过仓库直接拉取MetaGPT的好处是你可以更加灵活的使用MetaGPT框架，根据MetaGPT提供的基础组件来做出更符合自己需求的Agent
通过在终端内运行下面的代码从MetaGPT仓库获取MetaGPT

```bash
git clone https://github.com/geekan/MetaGPT.git
cd /your/path/to/MetaGPT
pip install -e .
```

获取MetaGPT的内容就到这里为止，但MetaGPT官方还提供了更多的获取方式，包括使用Docker，以及获取可生成图表的更完整的版本，更多内容你都可以在MetaGPT的官方文档中获取

[MetaGPT官方文档](https://docs.deepwisdom.ai/zhcn/guide/get_started/installation.html#%E5%AE%89%E8%A3%85%E5%85%A8%E9%83%A8%E5%8A%9F%E8%83%BD)