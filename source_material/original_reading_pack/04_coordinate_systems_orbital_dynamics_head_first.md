# Coordinate Systems in Orbital Dynamics

> Reading order: 04 of 05  
> Purpose: Understand ECI, TEME and ECEF, why frames differ, and how a TLE-based position is converted to geographic coordinates.

**Original PDF:** `04_coordinate_systems_orbital_dynamics_head_first.pdf`

---

Coordinate Systems in
                                     Orbital Dynamics
     A Head First chapter: what the names mean, why they exist, and how a TLE becomes latitude and
                                               longitude

 Our practical goal
 Given a satellite's TLE and a requested time, predict where the satellite is in space, then determine where that position
 lies relative to Earth's surface.

 The central idea
 A coordinate system is a measuring arrangement: it defines an origin and directions for its axes. Different
 coordinate systems can describe the same physical position using different numbers.

            Read in order. Each technical term is introduced only when its job becomes necessary.

1. Start with the problem, not the abbreviations
 Suppose an operator asks: Where will this satellite be at 14:00 UTC? This can mean two related things:

 In space: What is its three-dimensional position and velocity at that instant?

 Relative to Earth: What latitude, longitude and altitude describe its position?
 The satellite has one physical position at a given instant. But the numbers used to describe it depend on the
 measuring system. The object is real; the coordinate system is our agreed way to measure it.

 A coordinate system has three essentials
 1. An origin: the point from which position is measured. Earth-centred frames have their origin at Earth's centre.

 2. Axes: three directions called X, Y and Z, usually perpendicular to one another.

 3. An orientation rule: what those directions point toward and whether they rotate over time.

 If the axis directions differ, the same physical position can have different X, Y and Z values.

 2. Why the same position can have different numbers
 Imagine a coin on a table. With one set of axes, the coin is one step to the right of the origin: coordinates (1, 0). Keep
 the coin still, but rotate the measuring axes. Its coordinates change, even though the coin has not moved.

 A satellite is the same in three dimensions. At one instant, its TEME coordinates and ECEF coordinates can differ
 because the two frames use differently oriented axes.
 A frame transformation is the mathematical operation that converts coordinates from one defined frame to
 another. It does not move the satellite.

 3. Why Earth's rotation matters
 Earth rotates roughly once per day. A grid attached to Earth's surface rotates with it. A space-oriented grid does not
 rotate with Earth's daily spin in the same way.

 A ground station in India stays at approximately the same latitude and longitude. But as Earth rotates, the station's
 direction from Earth's centre changes relative to a space-oriented grid.

 So to locate a satellite relative to a ground station or map, we must account for Earth's orientation at the time of interest.
 The satellite's predicted position and Earth's rotation are separate facts.
 SGP4 predicts the satellite's state in its specified frame. A coordinate transformation then expresses that
 state in a frame tied to Earth.

 4. Three names, three jobs
       Name                          What it means                                        Why it matters

       ECI                           A family of Earth-centred, space-oriented            Useful for describing orbital motion in axes
       Earth-Centred Inertial        frames. The exact axes depend on which ECI           that do not rotate with Earth's daily spin. ECI
                                     frame is meant.                                      is a family name, not one unique frame.

       TEME                          A specific reference frame used by the standard      Standard SGP4 gives the satellite's position
       True Equator, Mean            SGP4 model with TLEs.                                and velocity in TEME. Do not treat TEME as
       Equinox                                                                            identical to every ECI frame.

       ECEF                          Earth-centred axes that rotate with Earth. A point   Useful for expressing the satellite's position
       Earth-Centred, Earth-Fixed    fixed on Earth's surface has nearly constant         relative to Earth's surface and calculating
                                     ECEF coordinates.                                    latitude, longitude and altitude.

 Do we need all three in sequence? No. For the TLE-to-map path, the practical chain is TLE → SGP4 → TEME →
 Earth-fixed coordinates → latitude/longitude/altitude. ECI is useful background and may be used by other
 systems, but it is not an extra mandatory step here.

5. Equator and equinox: why are they mentioned?
 These are not extra coordinate systems. They help define the orientation of certain astronomical frames.

 Equator = a reference plane
 Earth's equator is the imaginary circle around Earth's middle. Extend it into a flat plane passing through Earth's centre:
 the equatorial plane.

 It gives astronomers a common plane from which to measure orbital inclination. For example, an inclination of 0° means
 the orbit lies in the chosen equatorial plane; 90° means it is polar relative to that plane.

 Equinox = a reference direction
 A plane alone does not say where angle zero begins. To measure an angle around the equatorial plane, we also need a
 reference direction. Astronomical coordinate conventions use an equinox-related direction for this purpose.

 The vernal equinox direction is associated with the Sun's apparent crossing of the celestial equator from south to north.
 It is determined through observations and astronomical models; there is no physical peg or painted line in space.

 That direction is not perfectly fixed forever. Earth's axis slowly changes orientation (precession) and has smaller
 variations (nutation), so astronomical frames specify conventions and dates.
 Keep the jobs separate: the equatorial plane gives a plane; the equinox-related direction provides a reference
 for orienting axes. Neither tells us the satellite's position by itself.

 Does equal day and night define the equinox?
 No. Around an equinox, day and night are approximately equal in length, but that is not the precise definition used to
 establish the astronomical reference direction. The equinox event is determined from the Sun's apparent crossing of the
 celestial equator. Sunrise/sunset definitions, atmospheric refraction and the Sun's apparent size mean many places do
 not experience exactly 12 hours of daylight on that date.

 6. What TEME specifically means
 TEME expands to True Equator, Mean Equinox. The name identifies the equator/equinox conventions used to orient
 this particular frame.

 It does not mean that the origin is the intersection of the equator and equinox, that the equinox is a physical point, or
 that TEME is exactly the same as every frame called ECI.

 TEME is Earth-centred. The equator/equinox terms relate to the orientation of its axes, not to the location of its origin.
 Standard SGP4 implementations output the satellite state in TEME. Therefore the transformation must start from TEME,
 not from a vague assumption that the output is generic ECI.

 You do not need to derive the astronomy behind TEME before understanding the workflow. For practical use, know the
 input/output frame and use a transformation designed for those exact frames.

 7. The complete TLE-to-map sequence
 1. TLE + requested time
 The TLE provides compact orbital parameters tied to an epoch. The requested time tells us when to predict the state.

 2. SGP4 propagation
 SGP4 applies the prescribed model to calculate position and velocity at that time.

 3. TEME state
 The result is a state vector: position (X, Y, Z) and velocity (Vx, Vy, Vz), expressed in TEME.

 4. TEME → Earth-fixed
 A frame transformation uses the appropriate time and consistent conventions to express the same position in an
 Earth-fixed frame. Some implementations use an intermediate pseudo-Earth-fixed frame; higher-accuracy work may
 account for additional Earth-orientation effects.

 5. Earth-fixed → geographic
 Using an Earth model such as the WGS-84 reference ellipsoid, software converts Earth-fixed Cartesian coordinates into
 geodetic latitude, longitude and altitude.

In compact form:
   TLE + time → SGP4 → TEME position/velocity → Earth-fixed position → latitude, longitude,
   altitude

 The software does not need to see the Sun or measure day length each time it converts a satellite position.
 The frame definitions and transformation algorithms are encoded in the software; time tells the transformation
 how the frames relate at the requested instant.

 8. What makes the conversion reliable?
 If you request positions at closely spaced times, the calculated ground track should normally change continuously. The
 conversion is mathematical and time-dependent, not a visual guess.

 Three things must be consistent:

 • Correct source frame: interpret standard SGP4 output as TEME.

 • Correct time: use the time corresponding to the propagated state and the conventions required by the transformation.

 • Correct destination and Earth model: transform to an Earth-fixed frame, then use a defined ellipsoid for geographic
 coordinates.

 If software confuses TEME with another ECI frame or uses incompatible time/frame conventions, the result can be
 wrong even if SGP4 itself ran correctly.

 9. Common confusions, corrected
 “ECI is one exact coordinate system.”
 ECI is a family label. The particular frame must be specified for precise transformations.

 “TEME is just another name for ECI.”
 No. TEME is a specific frame used with standard SGP4/TLE workflows.

 “Equinox is a physical mark in space.”
 No. It is a defined astronomical reference direction.

 “Equal day and night defines the equinox.”
 No. It is an approximate seasonal consequence, not the precise frame definition.

 “Changing coordinates means the satellite moved.”
 No. The same physical position can have different components in differently oriented frames.

 “Latitude and longitude are just X, Y, Z with new labels.”
 No. They are a different representation calculated from an Earth-fixed position and an Earth model.

 “All three frames must always be used.”
 No. Use only the frames required by the task. The TLE-to-geographic path uses TEME and an Earth-fixed frame.

 10. Check your mental model
 Q1. What is a coordinate system?
 A defined origin, axes, and a rule for their orientation and motion.
 Q2. Why can one satellite position have different X, Y, Z values?
 Because different frames use differently oriented axes; the physical position can stay the same.
 Q3. Why convert TEME to Earth-fixed coordinates?
 Because TEME is not tied to Earth's rotating surface, while geographic coordinates describe position relative to Earth.
 Q4. What job does the equator do?
 It supplies a reference plane, including the plane used to define orbital inclination.
 Q5. What job does the equinox direction do?
 It supplies a conventional reference direction for orienting certain astronomical axes and measuring angles.

Q6. What is the practical TLE prediction sequence?
 TLE + time → SGP4 → TEME state → Earth-fixed position → latitude, longitude and altitude.

 The chapter in six sentences
 1. A coordinate system measures position using a defined origin and axes.

 2. Different axes can give different coordinates for the same physical position.

 3. Standard SGP4 propagation of a TLE produces the satellite state in TEME.

 4. TEME is a specific frame; ECI is a family of space-oriented frames; ECEF rotates with Earth.

 5. The equator defines a reference plane, while the equinox-related direction helps orient axes.
 6. To locate the satellite on a map, transform TEME position to an Earth-fixed frame and calculate geodetic
 latitude, longitude and altitude.

 Scope note: This chapter builds the conceptual model. Precise implementations may use specific time scales, Earth-orientation conventions
 and intermediate frames. For operational accuracy, follow the documentation for the SGP4 and coordinate-transformation library in use.
