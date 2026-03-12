# Markdown 页面

这个页面使用 **MyST Markdown**，由 `myst-parser` 解析。

- 可以直接写 Markdown 标题、列表、代码块
- 也可以引用另一个 rst 页面：{doc}`rst-guide`

## 代码块

```python
def hello(name: str) -> str:
    return f"hello, {name}"
```

## Markdown 指令

:::{note}
这是一个用 MyST 写的提示框。
:::

## 公式与引用

下面这个公式带有标签 `eq:energy`，可以在 Markdown 里直接引用：{eq}`eq:energy`。

```{math}
:label: eq:energy

E_{\theta} = \frac{\braket{\Psi_{\theta}|\hat{H}|\Psi_{\theta}}}{\braket{\Psi_{\theta}|\Psi_{\theta}}},
```

如果你更习惯 LaTeX，也可以把它理解成和下面这段等价的公式内容：

```latex
\begin{equation}
    \label{eq:energy}
    E_{\theta} = \frac{\braket{\Psi_{\theta}|\hat{H}|\Psi_{\theta}}}{\braket{\Psi_{\theta}|\Psi_{\theta}}},
\end{equation}
```

## Markdown 文献引用

这里演示 Markdown 里的文献引用，例如见 Li 的工作[^li2025]。

## 在 Markdown 里嵌入 rst

```{eval-rst}
.. warning::

   这一段 warning 指令本身是 rst，
   但可以通过 ``eval-rst`` 嵌入到 Markdown 页面里。
```

[^li2025]: Z. Li, *Phys. Rev. Lett.* **135**, 210601 (2025).
