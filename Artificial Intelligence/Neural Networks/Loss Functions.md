# Neural Network Loss Functions

- **Measures performance**: how well the neural network's predictions match the true target values.
- **Guides optimization**: the loss function quantifies the error which the optimizer tries to minimize.

## Regression Loss Functions

- **Mean Squared Error (MSE)**: average squared difference between the predicted and true target values.
  - $L(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$
- **Mean Absolute Error (MAE)**: average absolute difference between the predicted and true target values.
  - $L(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|$

### Notes

| Actual | Predicted   | Error             |
| ------ | ----------- | ----------------- |
| $y_i$  | $\hat{y}_i$ | $y_i - \hat{y}_i$ |

## Classification Loss Functions

- **Binary Cross-Entropy**: used for binary classification problems.
  - $L(y, \hat{y}) = - \frac{1}{n} \sum_{i=1}^{n} y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i)$
- **Categorical Cross-Entropy**: used for multi-class classification problems.
  - $L(y, \hat{y}) = - \frac{1}{n} \sum_{i=1}^{n} \sum_{j=1}^{m} y_{ij} \log(\hat{y}_{ij})$

### Notes

| Actual | Predicted   | Error                  |
| ------ | ----------- | ---------------------- |
| $y_i$  | $\hat{y}_i$ | $-y_i \log(\hat{y}_i)$ |

## Advanced Loss Functions

- **Huber Loss**: a combination of MSE and MAE that is less sensitive to outliers.
  - $L(y, \hat{y}) = \begin{cases} \frac{1}{2} a^2 & \text{if } |a| \leq \delta \\ \delta (|a| - \frac{1}{2} \delta) & |a| > \delta \end{cases}$
  - where $a = y_i - \hat{y}_i$
- **Hinge Loss**: used for maximum-margin classification, primarily in SVMs.
  - $L(y, \hat{y}) = \max(0, 1 - y_i \hat{y}_i)$
  - Where $y_i$ is the true label and $\hat{y}_i$ is the predicted score.

### Notes

- Huber Loss
  - Quadratic for small errors and linear for large errors.
- Hinge Loss
  - Penalizes only if $\text{margin} < 1$

## Regularization in Loss Functions

Prevents overfitting by adding a penalty term to the loss function.

$ \text{Regularized Loss} = \text{Original Loss} + \text{Regularization} $

### L1 Regularization (Lasso)

Adds the sum of the absolute weights to the loss function.

$L1(y, \hat{y}) = \lambda \sum_{i=1}^{n} |w_i|$

### L2 Regularization (Ridge)

Adds the sum of the squared weights to the loss function.

$L2(y, \hat{y}) = \lambda \sum_{i=1}^{n} w_i^2$

### Elastic Net Regularization

Combines L1 and L2 regularization.

$\text{ElasticNet} = \lambda_1 \sum_{i=1}^{n} |w_i| + \lambda_2 \sum_{i=1}^{n} w_i^2$
