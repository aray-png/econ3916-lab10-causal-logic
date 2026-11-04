# Abigail Ray || ECON 3916 || Correlation & Causality: Confounders, Colliders and the Limits of Controls

## Objective
I used simulations with known answers, plus the LaLonde job-training data, to show that a correlation alone cannot tell causation, confounding and selection apart, and that adding controls can either fix bias or create it.

## Methodology
- Simulated three worlds (true causation, pure confounding and pure selection) and compared their correlations and scatterplots against the true effects I had written into the code.
- Drew a confounder, a collider and a mediator as directed graphs with networkx, and read each one by its arrows.
- Ran regressions of Y on D with and without a control in three simulated cases: a confounder (good control), a collider (bad control) and an M-bias structure where the control is measured before treatment.
- Looked inside a slice of the collider to see why holding C fixed makes two independent variables look related.
- Wrote a function, `coef_on_d()`, that returns the coefficient on the treatment for any list of controls, and used it to control for W and u1 together.
- Reproduced the LaLonde contrast: the randomised experiment against a CPS comparison group, then measured how much of the gap covariate adjustment closes.
- For the take-home challenge, built the full graph in networkx, listed and classified every path between D and Y, and searched for the smallest valid adjustment set.

## Key Findings
- The three worlds had correlations of 0.654, 0.664 and 0.632, yet the true effects were 2.0, 0.0 and 0.0. The correlation alone could not tell them apart.
- With a confounder, the regression of Y on D alone gave 2.476 against a true effect of 1.5. Controlling for the confounder gave 1.500.
- With a collider, controlling for C gave -0.592 where the true effect is 0, with a p-value that printed as 0.000.
- In the M-bias setup, the regression without W gave 0.009 and the one with W, a control measured before treatment, gave -0.191, where the truth is 0. Controlling for u1 as well brought it to 0.006. This shows that "control for anything measured before treatment" is not a safe rule.
- In the LaLonde data, the experimental benchmark was $1,794 and the naive CPS comparison was -$8,498. With eight covariates as controls, the estimate was $699, which closed 89% of the gap.
- Getting close to the benchmark here does not prove the adjustment is valid. Without an experiment to check against, I would only see one number with nothing to tell me whether it is right.
- In the challenge, the graph search found that the smallest valid adjustment set is {U}, the confounder. The code could not tell me whether the graph itself is correct, and that is the hard part.
