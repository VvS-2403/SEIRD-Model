# AI use record: Member 3 (Vectorised Numerical Solvers and Benchmark Verification, Experiment E1)

**Tool:** Claude (Anthropic), accessed through Claude Code.

I decided what the solvers and the convergence experiment had to do, and I specified the tests and the pass criteria. Claude Code wrote first drafts of the solver code, the reference function, the notebook cells, the figure code and the method text. I ran every cell, read the output and checked the results myself.

## How I used it

| Part | My work | Where Claude helped | How it was checked |
|---|---|---|---|
| Vectorised Euler and RK4 | Chose to write both solvers from scratch as explicit fixed-step methods that update the whole 5-component state (s, e, i, r, d) at once with NumPy array operations, with a common `solve(f, y0, t, h)` interface. Specified that f takes the time-varying β(t) from Module 1's parameters. | Wrote the first draft of the vectorised Euler and RK4 loops and the docstrings. | Traced one step of each method by hand against the formulas. The orders in E1 match the theory. |
| Reference solution | Set up `reference_solution(params, t)` with SciPy's DOP853, shared with M4 and M5 so all three modules use one reference. Found in E1 that with rtol = 10⁻¹² the smallest RK4 errors reach the reference's own error of about 10⁻¹², and tightened it to rtol = 3 × 10⁻¹⁴ and atol = 10⁻¹⁶, close to the smallest SciPy allows. | Wrote the `solve_ivp` wrapper and the dense-output handling for arbitrary t. | With the tightened tolerances the RK4 order stays clean down to the smallest step (4.015). M4 and M5 call the same function. |
| E1 convergence experiment | Designed the experiment: six step sizes from h = 1 to 0.03125 days over t ∈ [0, 60] days, global error E(h) = max over steps and compartments of \|y_k − y_ref(t_k)\|, observed order log₂(E(h)/E(h/2)) for each pair, and a log-log fit with `np.polyfit`. | Wrote the loop over h and the order and `np.polyfit` code. | Fitted slopes over all six step sizes: Euler 1.001, RK4 4.085 (theory 1 and 4). Observed orders: 1.000 to 1.004 for Euler, 4.225 down to 4.015 for RK4. I recomputed the orders from the error table by hand. |
| Conservation check | Decided to check that s + e + i + r + d = 1 is preserved, and to treat it as a test that the code is correct, not a measure of accuracy. | Wrote the check cell. | Rounding is about 10⁻¹⁶ per step and builds up to about 10⁻¹⁵ at the smallest h (6.66 × 10⁻¹⁶ in the notebook), well inside the 10⁻¹² target. |
| Notebook and figures | Chose which figures and tables Module 3 needs: the E1 convergence plot (.eps) with reference slopes O(h) and O(h⁴), the E1 error and order table, and the figure comparing Euler's single slope with RK4's four slopes. Assembled the cells into the notebook and ran it in full in Google Colab. | Wrote the notebook cells and the matplotlib code for the convergence plot, the table and the Euler/RK4 slope figure. | Figures and table come from the final Colab run. The plot legend slopes (1.00 and 4.09) match the fitted values, and the plotted points match the table. |
| Writing and results | Decided which results to report (orders per pair of step sizes, fitted slopes, the accuracy gap at h = 1 day, conservation) and what they show, including why the RK4 order is slightly above 4 at large h. Revised the section until it matched the notebook. | Drafted the Module 3 text and its LaTeX: the two algorithms with their error orders, how accuracy is measured, why the total is conserved, and the interpretation of E1. | Every number in the text was checked against the final notebook. At h = 1 day RK4 is about 3 × 10⁴ times more accurate than Euler, for 4 times as many evaluations of f per step; I recomputed this ratio from the error table by hand. |

## What I checked

- Every Module 3 number in the report (convergence slopes, errors, conservation deviation) comes from the final notebook (`Final_MM_notebook.ipynb`) run in full in Google Colab. None was typed in by hand or by the AI.
- Euler and RK4 were checked against the formulas by hand for a single step, and against the reference solution over six step sizes (E1).
- The reference solution is the same function used by Modules 4 and 5, with the tolerances above.
- Other members' sections were not changed by this work.
