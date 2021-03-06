_The measures (and estimation techniques) implemented by this toolkit_

The JIDT implements a range of information-theoretic measures, for both _discrete_ and _continuous_-valued variables.

The measures (and estimation techniques) implemented by this toolkit are as follows

| Measure | Discrete | Continuous (implementation technique specified) |
| --- | --- | --- |
| **Entropy** | yes | (box) kernel estimation`*`, Kozachenko`*`, Gaussian`*` |
| **Entropy rate** | yes | _Use two multivariate entropy calculators_ |
| **Mutual information** | yes | Kraskov`*+`, (box) kernel estimation`*+`, Gaussian`*+`, Symbolic`*+`|
| **Conditional mutual information** | yes | Kraskov`*+`, Gaussian`*`, Symbolic`*+` |
| **Multi-information / Integration** | yes | Kraskov, (box) kernel estimation |
| **Transfer Entropy** | yes | Kraskov`*`, (box) kernel estimation`*`, Gaussian`*`, Symbolic |
| **Conditional/Complete Transfer Entropy** | yes | Kraskov`*`, Gaussian`*` |
| **Active information storage** | yes | Kraskov, (box) kernel estimation, Gaussian |
| **Predictive information / Excess entropy** | yes | Kraskov, (box) kernel estimation, Gaussian |
| **Separable information** | yes |  |

Key to table:
  * `*` indicates multivariate (i.e. joint state) implementation is provided.
  * `+` also implements MI from multivariate continuous variables to a discrete variable