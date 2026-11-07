# 7 IQD — Space Domain Learning Pack

This folder contains five distinct learning documents in a recommended sequence.
Each document is provided in two forms:

- **PDF** — original formatted reading copy.
- **Markdown (`.md`)** — text version for Git review, search and future editing.

## Recommended reading sequence

| Order | Document | Learning purpose |
|---:|---|---|
| 01 | [Satellite Orbit Tracking](01_Satellite_Orbit_Tracking_Head_First_One_Hour_Read.md) | Orbit geometry, six elements, orbital movement and ground track. |
| 02 | [Orbital Dynamics and Orbit Determination](02_orbital_dynamics_and_orbit_determination_fundamentals.md) | Earth motion, reference frames, tracking observations, orbit determination, propagation and ground-station passes. |
| 03 | [TLE and SGP4](03_understanding_satellite_orbits_TLE_SGP4_head_first.md) | Epoch, TLE structure, SGP4 and predicted satellite position/velocity. |
| 04 | [Coordinate Systems](04_coordinate_systems_orbital_dynamics_head_first.md) | ECI, TEME, ECEF, equator/equinox and coordinate transformation. |
| 05 | [From Space to Ground Track](05_head_first_reference_frames_ground_track.md) | Why the frame changes, geographic projection and a solved example. |

## Learning storyline

1. Understand the orbit and the satellite's position along it.
2. Understand how observations establish an estimated orbit and how that orbit is propagated.
3. Understand how the TLE and SGP4 work together to predict a satellite state.
4. Understand why the predicted state is expressed in TEME and why a map needs an Earth-fixed frame.
5. Connect the complete path to latitude, longitude and ground-track plotting.

## Important scope note

These are beginner learning notes, not operational procedures or validated flight-dynamics instructions. For real mission calculations, use the mission's specified reference frames, time standards, Earth-orientation conventions and validated software.

## Files

The numbered filenames preserve the recommended learning order. Keep the PDF and matching Markdown file together.
