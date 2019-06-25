# Latent_variable_regression
The algorithm improves the commonly used technique for parameterizing generalized Lotka-Volterra (GLV) equation. The most common approach for estimating GLV model parameters is to discretize the model, transform the discretized version to a set of linear equations, and obtain the optimal parameter values through linear regression. Since ecological field data is often noisy and infrequently sampled, the discretization error can be amplified by data uncertainty and leads to ineffective inference.

Our latent variable regression was built on the linear regression approach. The GLV model was also discretized but the log derivatives (or log difference) at the left-hand side of the discretized equations are iteratively learned in an optimization loop, rather than approximated by Euler's Method or high-order numerical methods. Due to the high uncertainty of log derivatives, they are essentially unobserved variables (i.e., latent variables). So we not only optimize the true variables (GLV model parameters), but also optimize latent variables (log derivatives).

The obtained best-fit parameters (we call it unperturbed solution) may not give stable coexistence of species at steady state. If we require that the ecosystem stably maintains all species at equilibrium, we can search the neighbourhood of the unperturbed solution in the parameter space and hopefully find alternative solutions that fit data equaly well but predict stable coexistence. This is technically achieved by using a slightly modified solution as initial guess (e.g., resample the self-interaction coefficients) and then run nonlinear optimization. Among all alternative solutions that predict stable coexistence, we choose the one with minimum model prediction error to finally parameterize the GLV model.

We implemented the latent variable regression algorithm in fish_network_inference.m and applid it to infer fish interaction network at La Grange pool of the Illinois River. The folder /scripts contains all MATLAB functions needed to run fish_network_inference.m and the folder /data contains input/output data of GLV inference. Should there be any questions, please contact Dr. Chen Liao through liaochen1988@gmail.com.
