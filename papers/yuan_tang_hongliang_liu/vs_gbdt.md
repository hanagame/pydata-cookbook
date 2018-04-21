# Title place holder (not to show in rst)
## XGBoost vs. GBDT

Gradient Boosting Decision Tree (short as "GBDT") is a type of boosting algorithm, which produces a weak learner (a decision tree) after each iteration and each tree is trained from the residual from last iteration. Each weak decision tree must be simple, has low variance and high bias, and each iteration improves the classification power by reducing the variance. Usually GBDT uses Classification And Regression Tree (CART). Since each tree must be simple, the tree can't be deep, and the output decision tree is the weighted summation of each weak tree.

CART as a binary tree at each iteration is generated by feature selection. For example, we can choose feature `j` from total `K` features as the first node to split the tree, and choose a value `v` as the threshold where two classes are determined by the split value `v` where one class is greater than `v` and the other less than `v`.

To find the optimal split value `v`, GBDT needs to sort all features values and this sorting is very time consuming. XGBoost sorts all features into blocks before training and keeps using these blocks during the training period for feature split. This pre-sorted blocks structure enables the key feature of XGBoost: parallelization where calculating the gain of each feature can be parallelized with these pre-sorted blocks.

Beyond parallelization, XGBoost also considers both the first order and the second order derivative of the loss function. Meanwhile, it includes tree trimming and regularization during the training. All of these ensures its better prediction power and less chance of overfitting than GBDT. 