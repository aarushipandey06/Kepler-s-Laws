# Numerical Verification of Kepler’s Second Law

## Objective

To investigate Kepler’s second law of planetary motion using numerical simulation and examine how the choice of numerical integration method and timestep affects the accuracy of the simulated orbit.

Kepler’s second law states that the line joining a planet and the Sun sweeps out equal areas in equal intervals of time. This is equivalent to conservation of angular momentum for motion under a central force.

## Physical Model

The planet is modelled as a body moving under the gravitational attraction of the Sun. The Sun is assumed to remain fixed at the origin, and the planet’s motion is treated as a two-dimensional problem.

Using Newton’s law of gravitation, the equations of motion are

$$
\frac{d^2x}{dt^2} = -\frac{\mu x}{r^3}
$$

$$
\frac{d^2y}{dt^2} = -\frac{\mu y}{r^3}
$$

where

$$
r = \sqrt{x^2+y^2}, \qquad \mu = GM
$$

Here, $r$ is the distance between the planet and the Sun, and $\mu$ is the gravitational parameter.


The simulation uses astronomical units (AU) for distance and years for time, with \(\mu=4\pi^2\) for the idealised solar system.

The model assumes:
- The Sun is stationary and its gravitational influence dominates.
- The planet’s mass is negligible compared with the Sun’s mass.
- Other planets, perturbations and relativistic effects are neglected.
- The orbit is determined by the initial position and velocity.

## Numerical Methods

Three numerical integration methods are investigated.

### 1. Euler Method

Euler’s method updates position and velocity using the current velocity and acceleration. It is simple to implement, but its errors can accumulate over time and affect the simulated orbit.

### 2. Fourth-Order Runge–Kutta (RK4)

RK4 evaluates the system at multiple intermediate points during each timestep to obtain a more accurate update. It generally achieves higher accuracy than basic Euler integration for a sufficiently small timestep.

### 3. Velocity Verlet

Velocity Verlet updates position and velocity using the acceleration at the current and subsequent positions. It is commonly used in mechanics simulations because of its favourable long-term energy behaviour for suitable conservative systems.

The methods are compared using the same physical model and initial conditions wherever applicable.

## Verification of Kepler’s Second Law

The swept area over a short timestep is approximated using the triangle formed by the Sun and the planet’s positions at successive timesteps:

\[
\Delta A \approx \frac{1}{2}
\left|x_i y_{i+1}-y_i x_{i+1}\right|.
\]

The corresponding approximate areal velocity is

\[
K_i=\frac{\Delta A}{\Delta t}.
\]

If Kepler’s second law is satisfied, the areal velocity should remain approximately constant. The simulated values are examined over time and compared with the theoretical areal velocity for an elliptical orbit:

\[
K_{\mathrm{theory}}=
\frac{1}{2}\sqrt{\mu a(1-e^2)},
\]

where \(a\) is the semi-major axis and \(e\) is the orbital eccentricity.

## Validation Against JPL Reference Data

The Earth-orbit simulation is also compared with reference state data from NASA/JPL Horizons.

The initial position and velocity are taken from the reference state at the chosen epoch. The simulated trajectory is then compared with the reference trajectory over the selected validation interval.

The position error is calculated as

\[
\text{Position Error (\%)}=
\frac{\left|\mathbf r_{\mathrm{sim}}-\mathbf r_{\mathrm{ref}}\right|}
{\left|\mathbf r_{\mathrm{ref}}\right|}\times100.
\]

Here, \(\mathbf r_{\mathrm{sim}}\) and \(\mathbf r_{\mathrm{ref}}\) are the simulated and reference position vectors, respectively.

The reference epoch, time interval, coordinate conventions and numerical error metrics should be specified alongside the results to make the comparison reproducible.

## Results and Analysis

The analysis focuses on three aspects:

1. **Verification of equal areas:** The variation of areal velocity is examined to assess how closely the numerical trajectory follows Kepler’s second law.
2. **Timestep dependence:** Simulations with different timesteps are compared to investigate how the timestep affects numerical accuracy.
3. **Integration-method comparison:** Euler, RK4 and Velocity Verlet are compared using the same clearly defined error metrics.

### Selected Figures

Add your actual generated plots here:

- `plots/orbit.png` — Simulated orbital trajectory.
- `plots/areal_velocity.png` — Areal velocity as a function of time.
- `plots/position_error.png` — Position error relative to JPL reference data.
- `plots/timestep_comparison.png` — Numerical error for different timesteps or integration methods.

Only include figures that you have generated and verified.

### Quantitative Results

Record the actual results from your simulation, including:
- The timestep used for each run.
- The maximum or final position error over the specified interval.
- The metric used to assess areal-velocity variation.
- The integration method used for each comparison.

Do not compare results using different error definitions or validation intervals without explicitly stating the differences.

## Limitations

The simulation uses a simplified two-body model and therefore does not account for perturbations from other planets or other effects included in high-precision orbital calculations.

Numerical accuracy depends on the timestep and integration method. A smaller timestep can reduce discretisation error, but it increases computational cost and does not eliminate all modelling or numerical errors.

The swept-area calculation is also an approximation over a finite timestep. Consequently, the measured areal velocity can vary slightly even when the underlying continuous physical model conserves angular momentum.

## Conclusion

This project uses numerical integration to investigate Kepler’s second law and examine the accuracy of simulated planetary motion. By comparing integration methods, varying the timestep and validating the simulated Earth orbit against JPL reference data, the project explores the relationship between physical modelling, numerical methods and computational accuracy.

## Tools

- Python
- NumPy
- Matplotlib
- Google Colab
- NASA/JPL Horizons reference data

## Reproducibility

The simulation notebook and supporting figures are provided in this repository. The initial conditions, timestep, integration method and validation interval should be documented so that the results can be reproduced and independently checked.
