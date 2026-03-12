reStructuredText 页面
======================

这个页面使用 ``.rst`` 语法。

- 可以放到同一个 ``toctree`` 里
- 也可以跳转到 Markdown 页面：:doc:`markdown-guide`

.. note::

   这是一个 rst 写法的 note 指令。

公式引用
--------

这里引用 Markdown 页面里的公式 :eq:`eq:energy`。

rst 数学公式
------------

下面这个公式直接写在 rst 页面里，并带有标签 :eq:`eq:Ham`。

.. math::
   :label: eq:Ham

   \hat{H} = \sum_{pq}h_{pq}\hat{a}_p^{\dagger}\hat{a}_q
   + \frac{1}{4} \sum_{pqrs}\braket{pq\| rs}\hat{a}_{p}^{\dagger}\hat{a}_q^{\dagger} \hat{a}_s\hat{a}_r

with :math:`h_{pq}` and :math:`\langle pq\|rs\rangle` being one-electron terms.

rst 文献引用
------------

这里演示 rst 里的文献引用，例如见 Li 的工作 [#li2025]_。

.. [#li2025]  Z. Li, *Phys. Rev. Lett.* **135**, 210601 (2025).

代码示例
--------

.. code-block:: python

   from pathlib import Path

   print(Path.cwd())
