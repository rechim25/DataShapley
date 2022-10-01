## Interface Summary

`DShap` object - encapsulates functionalities of TMC- and G-Shapley, as well as LOO.
- `X`: Data covariates.
- `y`: Data labels.
- `X_test`: Test+Held-out covariates.
- `y_test`: Test+Held-out labels.
- `sources`: An array or dictionary assiging each point to its group.
If None, evey points gets its individual value.
- `samples_weights`: Weight of train samples in the loss function.
(for models where weighted training method is enabled).
- `num_test`: Number of data points used for evaluation metric. The last num_test data points in the test set
are used as holdout test set to evaluate the performance plot. The rest becomes the test set on which we
compute the evaluation metric when running TMC-, G-Shapley and/or LOO.
- `directory`: Directory to save results and figures.
- `problem`: "Classification" or "Regression"(<em>Not implemented yet</em>).
- `model_family`: The model family used for learning algorithm. Allows for custom 
models as long as they implement the `fit()`.
- `metric`: Evaluation metric. Can be any function that takes  the 3 following arguments
in this order: model, X, y.
- `seed`: Random seed. When running parallel monte-carlo samples,
we initialize each with a different seed to prevent getting
same permutations.
- `overwrite`: Delete existing data and start computations from
scratch.
- `**kwargs`: Arguments of the model.

Notes on above parameters:
- `model_family` parameter can also take the following pre-defined values: `logistic`,
  `Tree`, `RandomForest`, `GB`, `AdaBoost`, `SVC`, `LinearSVC`, `GP`, `KNN`, `NB`, `linear`,
  `ridge`, `conv`, `conv_reg`, `NN`, `NN_reg`.
- `metric` parameter can also take: `accuracy`, `f1`, `auc`, `xe`.


`run()`- Calculates DSHAP values for every data source in the dataset.
- `save_every`: save marginal contributions every n iterations.
- `err`: stopping criteria (convergence).
- `tolerance` (default `0.01`): Truncation tolerance. If None, it's computed.
- `g_run` (default `True`): If True, computes G-Shapley values.
- `loo_run`(default `True`): If True, computes and saves leave-one-out scores.


`save_results()`- Saves results computed so far.
- `overwrite` (default `False`): Overwrites results if they already exist.
