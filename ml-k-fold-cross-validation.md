# K Fold cross-validation

Cross validation is a method to split randomly data in test / train folds and then to test each possible combination between test / train folds. This way we are sure that we have better estimation on the trained model.

## Example of K fold cross validation

```python
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LinearRegression
import numpy as np

# X = data
# y = target

k_folds = 7

linear_regression = LinearRegression()

scores_list = cross_val_score(linear_regression, X, y, cv = k_folds)
mean_scores = np.mean(scores_list)

print(scores)
print(mean_scores)
```