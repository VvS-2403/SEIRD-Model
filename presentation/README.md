# Presentation slides

Each module has its own folder with its Beamer frames, a standalone file to preview them, the compiled preview, and only the figures its slides use.

| Folder | Frames | Figures |
|---|---|---|
| `module1/` | Why β(t); published models (text only); phase plane and the peak; herd immunity and the control threshold (4 frames) | `m1_phase_space.png` (copy of the report figure) |
| `module2/` | R0 and stability; final size; sensitivity (3 frames) | `m2_final_size.png`, `m2_prcc.png` (copies of the report figures) |
| `module3/` | Solvers; conservation and accuracy checks; E1 convergence (3 frames) | `fig_e1_convergence.png` |
| `module4/` | PINN design; loss and training; synthetic E2-E4 (3 frames) | `fig_e2_forward_pinn.png`, `fig_e3_inverse_beta.png`, `fig_e4_hidden_states.png` |
| `module5/` | E5 held-out forecast; E7 rolling forecasts; what the PINN adds (3 frames) | `e5_cases.png`, `e5_deaths.png`, `e5_rt.png`, `e7_rolling.png` |

**Preview one module:** compile `moduleN/moduleN_standalone.tex` with pdflatex from inside its folder.

**Main deck:** compile `main_slides.tex` with pdflatex from this folder (run twice). It has a title slide, then the 16 module frames in order; all five modules are `\input` and `\graphicspath` covers each module folder.

All numbers on the slides come from `report/main.tex` (final Colab run).
