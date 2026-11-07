# Orbital Dynamics and Orbit Determination Fundamentals

> Reading order: 02 of 05  
> Purpose: Connect Earth motion, reference frames, orbital elements, tracking observations, orbit determination, propagation and ground-station passes.

**Original PDF:** `02_orbital_dynamics_and_orbit_determination_fundamentals.pdf`

---

ORBITAL DYNAMICS
                         AND ORBIT DETERMINATION
  A practical beginner’s guide to Earth geometry, reference frames, satellite orbits, tracking and
                                      ground-station passes

 What this guide covers
 How a satellite moves; how its position is expressed in a reference frame; what an equinox-based system means; how
 orbit determination differs from orbit propagation; and how a predicted orbit becomes a ground-station contact window.

   Read in sequence. Build the physical picture first; use the formal references at the end after the main
   concepts make sense.

 Focused study material • Not an operational procedure for commanding a real spacecraft

How to use this guide
 This is a focused study note for understanding the engineering behind satellite tracking, pass scheduling and
 command-contact planning. It is not a general astronomy textbook.

   • First: Understand Earth’s motions and the different angles.

   • Next: Learn reference frames and orbital elements.

   • Then: Connect orbit determination, propagation and pass prediction.

   • Finally: Use the external references for formal definitions and data formats.
   One rule to remember: whenever you see an angle, position or orbit, ask “relative to what?”

 1. Earth and satellite motion
 Three motions are easy to confuse, but they answer different questions:

   Concept                      Meaning                                                 Why it matters

   Earth’s rotation             Earth spins around its axis, taking about 23 h 56 min   A ground station moves with Earth; visibility changes
                                relative to distant stars.                              continuously.

   Earth’s revolution           Earth travels around the Sun once per year.             Defines the ecliptic plane and seasonal Sun geometry.

   Satellite orbit              A spacecraft moves around Earth under gravity and       Determines position, velocity, ground track and possible
                                other forces.                                           contact windows.

 Earth’s axial tilt: about 23.44°
 Earth’s spin axis is tilted by about 23.44° from the perpendicular to the ecliptic plane—the plane of Earth’s orbit around
 the Sun. This tilt explains the seasons. It is not the inclination of a satellite’s orbit.

 Satellite orbital inclination
 Orbital inclination, written i, is the angle between the satellite’s orbital plane and Earth’s equatorial plane. In ideal
 geometry, the subsatellite point reaches maximum latitudes of approximately +i and −i. A near-polar orbit has inclination
 near 90°.
   Example: an orbit with inclination 30° does not reach latitudes beyond roughly 30° north or south in the
   idealised geometry. A near-polar orbit can pass over a wide range of latitudes.

   Angle                                Measured relative to                              Question it answers

   Earth axial tilt (~23.44°)           Perpendicular to the ecliptic                     Why does Earth have seasons?

   Orbital inclination (i)              Earth’s equatorial plane                          How is the orbital plane tilted?

   Ground-station elevation             Local horizon                                     How high is the satellite above the station’s horizon?

   Solar elevation                      Local horizon                                     How high is the Sun in the sky?

 2. Reference frames: where are the axes?
 Coordinates are meaningful only when you know the origin, axis directions, frame and time. A position such as x =
 4,000 km, y = 3,000 km, z = 5,000 km is incomplete unless its reference frame is specified.

 ECI — Earth-centred inertial
   • Origin: near Earth’s centre of mass.

   • Axes: approximately non-rotating relative to a specified celestial reference.

   • Use: describing orbital position and velocity for propagation.

   • Note: ECI is a general label, not one unique frame. The precise frame definition matters.

ECEF / ITRF — Earth-fixed coordinates
   • Origin: Earth’s centre of mass.

   • Axes: rotate with Earth.

   • Use: ground-station coordinates, maps, latitude/longitude and ground tracks.

   • Note: ITRF is a family of realisations of the International Terrestrial Reference System; ECEF is a common generic
     name for Earth-fixed Cartesian coordinates.
   Practical connection: an orbit may be propagated in an inertial frame, then transformed into an Earth-fixed
   frame to calculate the satellite’s position relative to a ground station.

 3. What is an equinox-based reference system?
 The equinox is a geometrically defined direction associated with the intersection of the celestial equator and the
 ecliptic. It is not a physical marker in space.

   • Celestial equator: Earth’s equatorial plane extended outward into space.

   • Ecliptic: the plane of Earth’s orbit around the Sun, in the standard geometric description.

   • Equinox direction: a conventional reference direction at the intersection of the celestial equator and ecliptic.

   • Right ascension: an angular coordinate measured along the celestial equator from a specified equinox direction.

 J2000.0 and EME2000
 J2000.0 is a reference epoch: 1 January 2000 at 12:00 TT (Terrestrial Time), Julian Date 2451545.0 TT. EME2000 is an
 equinox-based celestial reference frame whose orientation is defined using the mean equator and mean equinox at that
 epoch.
   J2000 does not mean every orbit is calculated for the year 2000. It identifies a reference epoch/orientation.
   Earth’s orientation changes over time through precession, nutation, rotation irregularities and polar motion,
   so accurate systems must specify the frame and apply appropriate transformations.

 4. The six classical orbital elements
 In the ideal two-body model, six Keplerian elements describe the size, shape, orientation and position of an orbit at a
 specified epoch. Real operational orbit products may instead provide a state vector or an ephemeris.

   Element                      Meaning                                                               Remember it as

   Semi-major axis (a)          Orbit size; half the major axis of an ellipse.                        How large is the orbit?

   Eccentricity (e)             Shape: 0 is circular; between 0 and 1 is elliptical.                  How stretched is it?

   Inclination (i)              Orbital-plane tilt relative to the equator.                           How far north/south can the ground track
                                                                                                      reach?

   RAAN (Ω)                     Orientation of the ascending node relative to the selected inertial   Where does it cross the equator
                                reference direction.                                                  south-to-north?

   Argument of perigee (ω)      Angle from ascending node to perigee in the orbital plane.            Where is the closest point within the plane?

   True anomaly (ν)             Angular position from perigee at the epoch.                           Where is the satellite along the orbit?

 For a perfectly circular orbit, perigee is not uniquely defined, so some classical angular elements become ambiguous. Other element sets
 may be more suitable.

 5. How orbital motion evolves
 Gravity is the main force curving a satellite’s path. In the ideal two-body model, a bound Earth orbit is an ellipse; a circle
 is a special case.

Orbital period
 For a two-body orbit, the period depends mainly on semi-major axis: T = 2π√(a³/µ), where µ is Earth’s gravitational
 parameter. A larger semi-major axis generally means a longer orbital period. This relation explains the trend; it is not a
 complete operational propagation model.

 Why a real orbit changes
   • Earth’s non-spherical gravity: the equatorial bulge causes long-term changes, including drift in RAAN.

   • Atmospheric drag: important in low Earth orbit; it removes orbital energy and typically lowers the orbit.

   • Third-body gravity: the Moon and Sun perturb the orbit.

   • Solar radiation pressure: sunlight exerts a small force.

   • Manoeuvres: planned thrust changes the spacecraft’s state.
   A simple model is useful for learning geometry. Reliable pass scheduling requires suitable orbital data and
   a propagation model appropriate to the mission.

 6. Orbit determination versus orbit propagation
   Process                        Main question                                    Conceptual input → output

   Orbit determination (OD)       What is the best estimate of the actual          Observations + models → estimated position, velocity and
                                  orbital state?                                   uncertainty at an epoch.

   Orbit propagation              Where will the satellite be later according to   Initial state + time + force model → predicted state or ephemeris.
                                  the model?

   Pass prediction                When will it be visible from this station?       Predicted state + station location + Earth orientation + visibility
                                                                                   rules → contact windows.

   OD is an estimation problem. Propagation is a prediction problem. A plausible-looking trajectory does not
   by itself prove that the estimated orbit matches the actual spacecraft.

 What observations can support OD?
   • Range: distance between the station and spacecraft.

   • Range rate / Doppler: information about relative radial motion from the signal.

   • Angles: measured line-of-sight direction.

   • GNSS measurements: when the spacecraft carries and uses suitable GNSS equipment.

   • Other mission-specific observations: depend on the spacecraft and OD system.

 Different missions use different observations and estimation methods; no single measurement type is mandatory for
 every satellite.

 7. From orbit to a ground-station pass
 A pass occurs when the satellite meets a station’s visibility conditions. Being geometrically above the horizon does not
 automatically guarantee a usable communication link.

   • Station coordinates: latitude, longitude and height in a specified terrestrial frame.

   • Consistent time: the satellite state and station geometry must be evaluated at compatible times.

   • Frame transformation: express the satellite position in an Earth-fixed frame, accounting for Earth orientation as
     required by the accuracy target.

   • Station-relative geometry: calculate the line of sight, then azimuth and elevation.

   • Visibility mask: AOS and LOS may be defined by crossing a minimum elevation, not necessarily the exact horizon.

   • Operational constraints: station availability, antenna limits, link margin, conflicts and mission rules can reduce the
     usable window.

AOS and LOS
 AOS means Acquisition of Signal; LOS means Loss of Signal. In pass planning, these usually refer to predicted contact
 boundaries under a defined elevation mask and other assumptions. A scheduler may require margins for antenna setup
 and teardown.
   Do not confuse a communication pass with an Earth-observation opportunity. Payload visibility may
   additionally depend on target location, illumination, swath, imaging mode and spacecraft pointing.

 8. Where command uplink fits
 A pass schedule identifies a predicted communication opportunity. It does not guarantee that a command will be
 received or executed. Exact procedures depend on the mission and spacecraft.

   Stage                               Meaning

   Command preparation                 An authorised command is selected, parameterised, checked and entered into the command system.

   Contact planning                    A suitable station and communication window are selected with required constraints and margins.

   Transmission                        The ground station sends the command over the uplink.

   Reception / acceptance              The spacecraft or onboard software may report receipt, validation or acceptance according to its protocol.

   Execution                           The onboard system performs the command at the specified time or when required conditions are met.

   Verification                        Telemetry or other defined evidence confirms the intended outcome.

   Keep these states distinct: transmitted ≠ received ≠ accepted ≠ executed ≠ verified.

 9. Worked conceptual example
 Suppose a tracking system estimates the satellite’s state at a known epoch. The mission propagates that state forward
 and predicts a contact window for a ground station.

   • The propagated orbit predicts the satellite’s position at future times.

   • A reference-frame transformation relates the position to Earth and the station.

   • Station-relative geometry gives azimuth and elevation over time.

   • The visibility rule determines the predicted contact start and end.

   • The command system plans an authorised transmission during a suitable window.

   • Telemetry or protocol-specific evidence is used to verify receipt and execution.
   If orbit data are stale, the frame is misidentified, time conventions are inconsistent or station constraints are
   wrong, the predicted contact window may be wrong even if the scheduling software runs correctly.

 10. Recommended non-NASA references
 These are further-study references. Some are web pages rather than downloadable PDFs. The CCSDS document is a
 formal PDF standard. Treat standards as technical references, not as substitutes for a mission’s approved operating
 procedures.

 ESA Navipedia — Reference Systems and Frames
 Celestial and terrestrial reference systems and frames.

 https://gssc.esa.int/navipedia/index.php/Reference_Systems_and_Frames

 ESA Navipedia — Conventional Celestial Reference System
 Celestial axes and conventional reference-system definitions.

 https://gssc.esa.int/navipedia/index.php?title=Conventional_Celestial_Reference_System

CCSDS — Orbit Data Messages, CCSDS 502.0-B-3 (PDF)
 Formal format for exchanging orbit data, frames, epochs and ephemerides.

 https://ccsds.org/Pubs/502x0b3e1.pdf

 ESA — Packet Telecommand Standard PSS-04-107 (PDF)
 Specialised older reference for packet telecommand structure; not a current mission procedure.

 https://microelectronics.esa.int/vhdl/pss/PSS-04-107.pdf

 ESA — Telemetry and Telecommand
 Introductory context on command and telemetry functions.

 https://www.esa.int/Enabling_Support/Space_Engineering_Technology/Onboard_Computers_and_Data_Handling/Telemetry_Telecomman
 d

 11. Knowledge check
 What is the difference between Earth’s axial tilt and orbital inclination?
 Answer: Axial tilt is measured relative to the perpendicular to the ecliptic; satellite inclination is measured relative to Earth’s equatorial
 plane.

 Why must a position specify its reference frame?
 Answer: The origin, axes, orientation and epoch define what the coordinates mean.

 What is the difference between OD and propagation?
 Answer: OD estimates the state from observations; propagation predicts the state at future times from a starting state and model.

 Why transform to an Earth-fixed frame for a ground-station pass?
 Answer: The station is fixed to Earth, so the transformation enables station-relative geometry.

 Does AOS guarantee command success?
 Answer: No. It is a predicted contact boundary under defined assumptions.

 Does command transmission prove execution?
 Answer: No. Transmission, reception, acceptance, execution and verification are separate states.

 12. Suggested study sequence
   Session             Read                                 Outcome

   1                   Sections 1–3                         Explain axial tilt, inclination, ECI/ECEF and equinox/J2000.

   2                   Sections 4–6                         Explain orbital elements and distinguish OD from propagation.

   3                   Section 7                            Explain how a predicted orbit becomes AOS/LOS and azimuth/elevation.

   4                   Section 8                            Explain why a contact opportunity does not guarantee command execution.

   5                   External references                  Look up frames, epochs, state vectors and orbit-data formats.

 Scope note: This is a conceptual study guide. Real orbit determination, propagation, pass scheduling and telecommand require
 mission-specific data, validated software, explicit time/frame conventions and authorised operational procedures.
