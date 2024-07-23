
Uniform Manifold Approximation with Two-phase Optimization (UMATO) is a dimensionality reduction technique designed to preserve both the global and local structures of high-dimensional data. Most existing dimensionality reduction algorithms focus on either global or local structure, which can lead to overlooking or misinterpreting important patterns in the data. Additionally, many existing algorithms suffer from instability.

To address these issues, UMATO introduces a two-phase optimization process: global optimization and local optimization. The global structure is obtained by selecting and optimizing hub points, and then the local structure is refined by initializing and optimizing other points using the nearest neighbor graph. This approach ensures a balanced preservation of global and local structures while maintaining stability.

This demo showcases the effectiveness of UMATO in various datasets, demonstrating its capability to outperform previous algorithms in terms of accuracy, stability, and scalability.

You can learn more about UMATO by visiting the [UMATO](https://github.com/hyungkwonko/umato) GitHub repository.

## Citation

UMATO can be cited as follows:

```bibtex
@inproceedings{jeon2022vis,
  title={Uniform Manifold Approximation with Two-phase Optimization},
  author={Jeon, Hyeon and Ko, Hyung-Kwon and Lee, Soohyun and Jo, Jaemin and Seo, Jinwook},
  booktitle={2022 IEEE Visualization and Visual Analytics (VIS)},
  pages={80--84},
  year={2022},
  organization={IEEE}
}
```

Jeon, H., Ko, H. K., Lee, S., Jo, J., & Seo, J. (2022, October). Uniform Manifold Approximation with Two-phase Optimization. In 2022 IEEE Visualization and Visual Analytics (VIS) (pp. 80-84). IEEE.
