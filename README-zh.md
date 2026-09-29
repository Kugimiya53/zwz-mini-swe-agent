<div align="center">
<a href="https://mini-swe-agent.com/latest/"><img src="https://github.com/SWE-agent/mini-swe-agent/raw/main/docs/assets/mini-swe-agent-banner.svg" alt="mini-swe-agent banner" style="height: 7em"/></a>
</div>

# 极简 AI 软件工程智能体

📣 [mini-swe-agent 现已为 Ramp SWE-Bench 提供支持](https://labs.ramp.com/swebench)<br/>
📣 [mini-swe-agent 在 DeepSWE 上击败 Claude Code 和 Codex](https://deepswe.datacurve.ai/blog#evaluation-harness)<br/>
📣 [在我们全新且极具挑战性的 ProgramBench 基准测试上运行 mini-swe-agent](https://mini-swe-agent.com/latest/usage/programbench/)<br/>
📣 [关于构建极简 AI 智能体的新教程](https://minimal-agent.com/)

[![Docs](https://img.shields.io/badge/Docs-green?style=for-the-badge&logo=materialformkdocs&logoColor=white)](https://mini-swe-agent.com/latest/)
[![Slack](https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white)](https://join.slack.com/t/swe-bench/shared_invite/zt-36pj9bu5s-o3_yXPZbaH2wVnxnss1EkQ)
[![PyPI - Version](https://img.shields.io/pypi/v/mini-swe-agent?style=for-the-badge&logo=python&logoColor=white&labelColor=black&color=deeppink)](https://pypi.org/project/mini-swe-agent/)

> [!WARNING]
> 这是 **mini-swe-agent v2**。请阅读[迁移指南](https://mini-swe-agent.com/latest/advanced/v2_migration/)。如需使用之前的版本，请查看 [v1 分支](https://github.com/SWE-agent/mini-swe-agent/tree/v1)。

2024 年，我们构建了 [SWE-bench](https://github.com/swe-bench/SWE-bench) 和 [SWE-agent](https://github.com/swe-agent/swe-agent)，并帮助开启了编码智能体革命。

现在我们要问：**如果我们的智能体简单 100 倍，却仍然几乎同样有效，会怎样？**

`mini` 具备以下特点：

- **广泛采用**：Meta、NVIDIA、Essential AI、IBM、Nebius、Anyscale、普林斯顿大学、斯坦福大学等众多机构都在使用。
- **极简**：[智能体类](https://github.com/SWE-agent/mini-swe-agent/blob/main/src/minisweagent/agents/default.py)只需大约 100 行 Python（另需少量代码用于[环境](https://github.com/SWE-agent/mini-swe-agent/blob/main/src/minisweagent/environments/local.py)、
[模型](https://github.com/SWE-agent/mini-swe-agent/blob/main/src/minisweagent/models/litellm_model.py)和[运行脚本](https://github.com/SWE-agent/mini-swe-agent/blob/main/src/minisweagent/run/hello_world.py)），没有花哨的依赖！
- **高性能**：在 [SWE-bench verified 基准测试](https://www.swebench.com/)上得分 >74%；启动速度远快于 Claude Code
- **可部署**：支持**本地环境**、**docker/podman**、**singularity/apptainer**、**bublewrap**、**contree** 等
- **兼容性强**：通过 **litellm**、**openrouter**、**portkey** 等支持所有模型。支持 `/completion` 和 `/response` 端点、交错思考等功能。
- 由普林斯顿大学和斯坦福大学团队构建，他们也是 [SWE-bench](https://swebench.com)、[SWE-agent](https://swe-agent.com) 等项目的幕后团队
- **经过测试**：[![Codecov](https://img.shields.io/codecov/c/github/swe-agent/mini-swe-agent?style=flat-square)](https://codecov.io/gh/SWE-agent/mini-swe-agent)

<details>

<summary>更多动机（面向研究）</summary>

[SWE-agent](https://swe-agent.com/latest/) 在 2024 年推动了 AI 智能体的发展。当时，我们非常重视工具以及为智能体设计的特殊接口。
然而，一年之后，随着 LM 能力不断增强，要构建一个有用的智能体，很多东西完全不再需要了！
事实上，`mini` 智能体

- **除了 bash 没有任何其他工具**，它甚至不需要使用 LM 的工具调用接口。
  这意味着你确实可以用任意模型运行它。在沙箱环境中运行时，你也不需要操心
  安装任何软件包，它只需要 bash。
- **拥有完全线性的历史记录**，智能体的每一步都只是追加到消息中，仅此而已。
  因此，轨迹和你传给 LM 的消息没有区别。
  非常适合调试和微调。
- **使用 `subprocess.run` 执行动作**，每个动作完全独立（而不是保持一个有状态的 shell 会话运行）。
  这让它可以轻松地在沙箱中执行动作（实际上只需将 `subprocess.run` 替换为 `docker exec`），并且可以
  毫不费力地扩展规模。说真的，这真是[一件大事](https://mini-swe-agent.com/latest/faq/#why-no-shell-session)，相信我。

这使它非常适合作为基线系统，也适合那些将注意力放在语言模型本身，而不是
智能体脚手架上的系统。
你可以在 [SWE-bench（仅 bash）](https://www.swebench.com/)排行榜上看到结果，该排行榜评估了不同 LM 配合 `mini` 的表现。

</details>

<details>
<summary>更多动机（作为工具）</summary>

有些智能体是过度拟合的研究产物，另一些则是 UI 繁重的前端怪物。

`mini` 智能体希望成为一个可改造的工具，而不是黑盒。

- **足够简单**，一眼就能看懂
- **足够方便**，可以用于日常工作流
- **足够灵活**，可以扩展

与其他智能体（包括我们自己的 [swe-agent](https://swe-agent.com/latest/)）不同，它极其简单，因为它：

- **除了 bash 没有任何其他工具**，它甚至不需要使用 LM 的工具调用接口。
  我们不为智能体可能想做的每一件具体事情实现自定义工具，而是完全专注于让 LM 充分发挥 shell 的潜力。
  想让它做一些特定的事情，比如创建 PR？
  直接告诉 LM 让它自己想办法，而不是花时间把这项功能实现到智能体中。
- **使用 `subprocess.run` 执行动作**，每个动作完全独立（而不是保持一个有状态的 shell 会话运行）。
  这对智能体的稳定性来说是[一件大事](https://mini-swe-agent.com/latest/faq/#why-no-shell-session)，相信我。
- **拥有完全线性的历史记录**，智能体的每一步都只是将消息追加到下一步传给 LM 的消息中，仅此而已。
  这非常适合调试，也有助于理解传给 LM 的提示内容。

</details>

<details>
<summary>我应该使用 SWE-agent 还是 mini-SWE-agent？</summary>

你应该把 `mini-swe-agent` 作为默认选择。
尤其是在以下情况下，你应该使用 `mini-swe-agent`：

- 你想要一个能在本地运行的快速命令行工具
- 你想要一个控制流非常简单的智能体
- 你想要更快、更简单、更稳定的沙箱和基准测试评估
- 你正在进行 FT 或 RL，不想过度拟合到特定的智能体脚手架

以下情况下，你应该使用 `swe-agent`：

- 你想试验不同的工具集合，每种工具都有自己的接口
- 你想试验不同的历史记录处理器

两者都能提供：

- 出色的 SWE-Bench 性能
- 轨迹浏览器

</details>

<table>
<tr>
<td width="50%">
<a href="https://mini-swe-agent.com/latest/usage/mini/"><strong>CLI</strong></a> (<code>mini</code>)
</td>
<td>
<a href="https://mini-swe-agent.com/latest/usage/swebench/"><strong>批量推理</strong></a>
</td>
</tr>
<tr>
<td width="50%">

![mini](https://github.com/SWE-agent/swe-agent-media/blob/main/media/mini/gif/mini.gif?raw=true)

</td>
<td>

![swebench](https://github.com/SWE-agent/swe-agent-media/blob/main/media/mini/gif/swebench.gif?raw=true)

</td>
</tr>
<tr>
<td>
<a href="https://mini-swe-agent.com/latest/usage/inspector/"><strong>轨迹浏览器</strong></a>
</td>
<td>
<a href="https://mini-swe-agent.com/latest/advanced/cookbook/"><strong>Python 绑定</strong></a>
</td>
</tr>
<tr>
<td>

![inspector](https://github.com/SWE-agent/swe-agent-media/blob/main/media/mini/gif/inspector.gif?raw=true)

</td>
<td>

```python
agent = DefaultAgent(
    LitellmModel(model_name=...),
    LocalEnvironment(),
)
agent.run("Write a sudoku game")
```

</td>
</tr>
</table>

## 开始使用！

**选项 1：**如果你只是想试用 CLI（软件包安装在匿名虚拟环境中）

```bash
pip install uv && uvx mini-swe-agent
# or
pip install pipx && pipx ensurepath && pipx run mini-swe-agent
```

**选项 2：**在当前环境中安装 CLI 和 Python 绑定

```bash
pip install mini-swe-agent
mini  # run the CLI
```

**选项 3：**从源代码安装（开发环境配置）

```bash
git clone https://github.com/SWE-agent/mini-swe-agent.git
cd mini-swe-agent && pip install -e .
mini  # run the CLI
```

请在我们的[文档](https://mini-swe-agent.com/latest/)中阅读更多内容：

* [快速入门指南](https://mini-swe-agent.com/latest/quickstart/)
* [使用 `mini` CLI](https://mini-swe-agent.com/latest/usage/mini/)
* [全局配置](https://mini-swe-agent.com/latest/advanced/global_configuration/)
* [Yaml 配置文件](https://mini-swe-agent.com/latest/advanced/yaml_configuration/)
* [通过 cookbook 增强功能](https://mini-swe-agent.com/latest/advanced/cookbook/)
* [常见问题](https://mini-swe-agent.com/latest/faq/)
* [参与贡献！](https://mini-swe-agent.com/latest/contributing/)

## 引用说明

如果这项工作对你有帮助，请考虑在你的工作中引用 [SWE-agent 论文](https://arxiv.org/abs/2405.15793)：

```bibtex
@inproceedings{yang2024sweagent,
  title={{SWE}-agent: Agent-Computer Interfaces Enable Automated Software Engineering},
  author={John Yang and Carlos E Jimenez and Alexander Wettig and Kilian Lieret and Shunyu Yao and Karthik R Narasimhan and Ofir Press},
  booktitle={The Thirty-eighth Annual Conference on Neural Information Processing Systems},
  year={2024},
  url={https://arxiv.org/abs/2405.15793}
}
```

我们的其他项目：

<div align="center">
  <a href="https://github.com/SWE-agent/SWE-agent"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/sweagent_logo_text_below.svg" alt="SWE-agent" height="120px"></a>
   &nbsp;&nbsp;
  <a href="https://github.com/SWE-agent/SWE-ReX"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/swerex_logo_text_below.svg" alt="SWE-ReX" height="120px"></a>
   &nbsp;&nbsp;
  <a href="https://github.com/SWE-bench/SWE-bench"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/swebench_logo_text_below.svg" alt="SWE-bench" height="120px"></a>
  &nbsp;&nbsp;
  <a href="https://github.com/SWE-bench/SWE-smith"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/swesmith_logo_text_below.svg" alt="SWE-smith" height="120px"></a>
  &nbsp;&nbsp;
  <a href="https://github.com/codeclash-ai/codeclash"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/codeclash_logo_text_below.svg" alt="CodeClash" height="120px"></a>
  &nbsp;&nbsp;
  <a href="https://github.com/SWE-bench/sb-cli"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/sbcli_logo_text_below.svg" alt="sb-cli" height="120px"></a>
</div>
