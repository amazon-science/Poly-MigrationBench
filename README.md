# Poly-MigrationBench
<table>
  <tr>
    <td style="padding: 0;">
      <a href="">
        <img src="https://img.shields.io/badge/-🤗 Poly--MigrationBench (coming soon)-4d5eff?style=flatten&labelColor" alt="Poly-MigrationBench">
      </a>
    </td>
    <td style="padding: 0;">
      <a href="https://github.com/amazon-science/MigrationBench">
        <img src="https://img.shields.io/badge/MigrationBench-000000?style=flatten&logo=github" alt="MigrationBench (GitHub)">
      </a>
    </td>
    <td style="padding: 0;">
      <a href="https://arxiv.org/abs/2505.09569">
        <img src="https://img.shields.io/badge/arXiv-2505.09569-b31b1b.svg?style=flatten" alt="MigrationBench (arXiv)">
      </a>
    </td>
  </tr>
</table>

<!--
npm install -g markdown-toc
markdown-toc -i README.md
-->


## 1. 📖 Overview

[Poly-MigrationBench](https://github.com/amazon-science/Poly-MigrationBench) is a follow-up work of [MigrationBench](https://github.com/amazon-science/MigrationBench). 

While [MigrationBench](https://github.com/amazon-science/MigrationBench) focuses exclusively on Java, the real-world code migration problem spans multiple ecosystems. To address this broader scope, we develop [Poly-MigrationBench](https://github.com/amazon-science/Poly-MigrationBench), an extension that introduces additional languages and platforms. We applied a similar data curation process as [MigrationBench](https://github.com/amazon-science/MigrationBench) to additionally collect

 - **100** .NET Framework repositories. The target is to be migrated to .NET core.
 - **74** Node.js repositories with Node.js version less than 22. The target is to be migrated to Node.js 22.
 - **83** Python repositories with Python version less than 3.13. The target is to be migrated to Python 3.13.

For more details on the problem formulation, dataset curation pipeline and evaluation framework, read our paper: [MigrationBench: Repository-Level Code Migration Benchmark from Java 8](https://arxiv.org/abs/2505.09569)


## 2. 📦 Dataset
There are three datasets in [Poly-MigrationBench](https://github.com/amazon-science/Poly-MigrationBench):
- All repositories included in the datasets are under the `MIT` or `Apache-2.0` license.

| Index | Dataset                                       | Size  | Notes                                                                                               |
|-------|-----------------------------------------------|-------|-----------------------------------------------------------------------------------------------------|
| 1     | [`Poly-MigrationBench-dotnet`](https://github.com/amazon-science/Poly-MigrationBench/Poly-MigrationBench-dotnet.csv)         | 100 | Under .NET Framework                              |
| 2     | [`Poly-MigrationBench-node`](https://github.com/amazon-science/Poly-MigrationBench/Poly-MigrationBench-node.csv)  |   74 | Under Node.js <= 20                                          |
| 3     | [`Poly-MigrationBench-python`](https://github.com/amazon-science/Poly-MigrationBench/Poly-MigrationBench-python.csv)           | 83 | Under Python <= 3.12|

## 3. 🧩 Metadata
Metadata is provided in the `csv` file for each dataset.

### 3.1 [`Poly-MigrationBench-dotnet`](https://github.com/amazon-science/Poly-MigrationBench/Poly-MigrationBench-dotnet.csv)

1. `repo (str)`: The original repo URL without the `https://github.com/` prefix
1. `base_commit (str)`: Base commit id
    - At this commit the repository is under .NET Framework. The repositories can build and pass unit tests
1. `num_cs_files (int)`: Number of `*.cs` files in the repository at `base_commit`
1. `root_sln_or_csproj_files (str)`: The list of `*.sln` and `*.csproj` files under the project root directory at `base_commit`. Files are separated by `;`
1. `verify_command (str)`: The command used to verify migration success, which is also the verifier `v` introduced in Section 3.1 of the paper [MigrationBench: Repository-Level Code Migration Benchmark from Java 8](https://arxiv.org/abs/2505.09569).
1. `license (str)`: The license of the repository, either MIT or Apache-2.0 for the whole dataset

### 3.2 [`Poly-MigrationBench-node`](https://github.com/amazon-science/Poly-MigrationBench/Poly-MigrationBench-node.csv)

1. `repo (str)`: The original repo URL without the `https://github.com/` prefix
1. `base_commit (str)`: Base commit id
    - At this commit the repository is under Node.js <= 20
1. `num_js_and_ts_files (int)`: Number of `*.js` and `*.ts` files in the repository at `base_commit`
1. `num_loc (int)`: Number of lines of code for `*.js` and `*.ts` files in the repository at `base_commit`
1. `num_unit_test (int)`: Number of unit tests
1. `install_command (str)`: The command used to install dependencies
1. `build_command (Optional[str])`: The command used to build the project and might be empty if there is no build command
1. `test_command (str)`: The command used to run unit tests
1. `deploy_command (Optional[str])`: the command used to deploy the AWS Lambda project and might be empty if there no deploy command. Depending on the migration goal, any non-empty combination of the `install_command`, `build_command`, `test_command`, or `deploy_command` can serve as the verifier `v` for migration success.
1. `license (str)`: The license of the repository, either MIT or Apache2.0 for the whole dataset


### 3.3 [`Poly-MigrationBench-python`](https://github.com/amazon-science/Poly-MigrationBench/Poly-MigrationBench-python.csv)

1. `repo (str)`: The original repo URL without the `https://github.com/` prefix
1. `base_commit (str)`: Base commit id
    - At this commit the repository is under Python <= 3.12
1. `num_files (int)`: ,num_loc,build_command
1. `num_py_files (int)`: Number of `*.py` files in the repository at `base_commit`
1. `num_loc (int)`: Number of lines of code for `*.py` files in the repository at `base_commit`
1. `license (str)`: The license of the repository, either MIT or Apache-2.0 for the whole dataset

## 4. 📚 Citation

```bibtex
@misc{liu2025migrationbenchrepositorylevelcodemigration,
      title={MigrationBench: Repository-Level Code Migration Benchmark from Java 8},
      author={Linbo Liu and Xinle Liu and Qiang Zhou and Lin Chen and Yihan Liu and Hoan Nguyen and Behrooz Omidvar-Tehrani and Xi Shen and Jun Huan and Omer Tripp and Anoop Deoras},
      year={2025},
      eprint={2505.09569},
      archivePrefix={arXiv},
      primaryClass={cs.SE},
      url={https://arxiv.org/abs/2505.09569},
}
```
