# Base-section quantities

Source: VC-BASE. This is the reviewed symmetric crushed-stone-base model, not a general earthwork or pavement design method.

- **[Math]** Convert compacted thickness from inches to feet before cross-sectional area; convert ft³ to yd³ by dividing by 27. Mass follows volume times a density expressed in the matching volume and explicitly identified mass unit. Keep waste/allowance separate from theoretical compacted quantity.
- **[Assumption/application]** The model uses pavement plus two shoulder widths, uniform thickness, two identical triangular keyouts, a base bottom following shoulder slope, and straight side-slope closure. It does not integrate variable terrain, cut/fill, asymmetric sections, or curved material boundaries.
- **[Math under that model]** Let `t` be thickness in feet, `W` total pavement-plus-shoulder width, `z` the side slope H:V, and `s` the shoulder slope as a positive downward decimal under this model. Keyout run `r=t/(1/z-s)` requires a positive denominator. Each triangular keyout has area `0.5*t*r`; total area is `t*W+2*(0.5*t*r)`. Multiply by the applicable length only where the section is constant.
- **[Safeguard]** Reject nonfinite/invalid widths, thickness, slopes, density, and length. Zero or negative closure denominator is an invalid/unbounded modeled keyout, not a reason to take an absolute value or clamp the run.
- **[Project/assumption]** Density, compacted versus loose state, moisture, waste, and the meaning of “ton” need specification. The application's default density is not a published material property or agency criterion.
- **[Validated, mathematical scope]** Hand-calculated area/volume cases and dimensional tests exercise the implementation. They verify the stated geometric model, not a material specification, actual measured pay quantity, or suitability of the modeled section.
