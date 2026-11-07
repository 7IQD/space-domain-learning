# Satellite Orbit Tracking — A Head First Guide

> Reading order: 01 of 05  
> Purpose: Build the physical picture of an orbit: size, shape, orientation, position along the orbit, and the ground track.

**Original PDF:** `01_Satellite_Orbit_Tracking_Head_First_One_Hour_Read.pdf`

---

A Head First guide for newcomers

                                 From orbit landmarks to “where is it now?”

               SIZE                                         SHAPE
               Semi-major axis (a)                          Eccentricity (e)

               TILT                                         TWIST
               Inclination (i)                              RAAN (Ω)

               ORBIT DIRECTION                              POSITION
               Argument of periapsis (ω)                    True anomaly (ν)

      Estimated reading time: 45–60 minutes, including the short checks and recap.

       The aim is not to memorise six names. It is to build a mental picture that lets you read a tracking
       display and understand what each number is telling you.

How to use this guide
     Read it in order. Each section answers one practical question, introduces only the terms needed for that
     answer, and then checks your understanding. Do not try to learn every orbital formula at once.

     One important idea: an orbit describes the path and its orientation; a position value tells you where the
     satellite is along that path at a particular time.

     The route through this guide
     • Part 1 — Build the picture: the six orbital elements and what each one answers.

     • Part 2 — Find the satellite: true anomaly, periapsis, apoapsis, and why the satellite speeds up and slows
     down.

     • Part 3 — Estimate the rhythm: orbital period and mean motion.

     • Part 4 — Read a map correctly: orbit in space versus ground track on a rotating Earth.

     • Part 5 — Put it together: a sample tracking display, common traps, and a self-check.

       Beginner’s rule: whenever a number appears on a tracking screen, ask: “Does this describe the
       orbit’s shape/orientation, the satellite’s current position, its timing, or its path over Earth?”

     1. First, separate the orbit from the satellite’s position
     Imagine drawing a large oval path around Earth. You can describe that oval without choosing where the
     satellite is on it at this instant. The oval has a size and shape, and it sits in a particular orientation in space.

     Now imagine a small marker moving around that oval. The marker is the satellite. Even if the path were
     unchanged, the marker would move every second. To track it, you need both the path description and a way
     to say where the marker is on the path.

     This is the core distinction:

       Orbit: the path the satellite follows.
       Position along the orbit: the satellite’s current place on that path.
       Ground track: the line traced on Earth’s surface below the satellite.

     The six classical Keplerian orbital elements describe an idealised orbit and the satellite’s location at a
     specified epoch (a reference time). They are not six permanently fixed labels. In real life, gravity from a
     non-perfect Earth, the Moon and Sun, and atmospheric drag can gradually change some elements.

     2. The six elements — six questions, not six
     definitions
     Use this memory aid: Size, Shape, Tilt, Twist, Periapsis direction, Position.

     Question                        Element                        Plain-English meaning

     How large is the orbit?         Semi-major axis (a)            The orbit’s overall size; strongly determines orbital period.

     How stretched is it?            Eccentricity (e)               The shape: 0 is circular; values closer to 1 are more
                                                                    stretched.

     How tilted is it?               Inclination (i)                The angle between the orbital plane and Earth’s equatorial
                                                                    plane.

Question                        Element                                Plain-English meaning

     Which way is the plane          RAAN (Ω)                               Sets the orientation of the orbital plane around Earth’s
     turned?                                                                polar axis, measured from a reference direction.

     Where is the closest point      Argument of periapsis (ω)              Orients the ellipse inside the orbital plane.
     within that plane?

     Where is the satellite on the   True anomaly (ν)                       An angle measured from periapsis to the satellite’s current
     path now?                                                              position, in the orbital plane.

     A small correction to the “static landmarks” idea
     For a first mental model, treat the first five elements as the orbit’s landmarks and true anomaly as the moving
     marker. That is useful over a short tracking interval. More precisely, the first five are not guaranteed to remain
     fixed for days or months: they can drift, and for a circular orbit periapsis is not uniquely defined. Also, true
     anomaly is not the only value that changes with time in software; time, coordinates, range, and other live
     outputs change too. It is the element that directly describes position along the ideal orbit.

     Check your understanding
     1. Which element tells you the orbit’s tilt? 2. Which element tells you the satellite’s place measured from the
        closest point? 3. If you know the orbit but not the time or position along it, what is missing?
     Answers: 1) inclination; 2) true anomaly; 3) the satellite’s current position along the orbit (and the epoch/time needed to propagate
     it).

     3. The two special points: periapsis and apoapsis
     For an elliptical orbit, the satellite does not remain the same distance from Earth. The closest point is called
     periapsis; the farthest point is apoapsis. Around Earth, people often use the terms perigee and apogee.
     “Periapsis/apoapsis” are general terms that work for orbits around any central body.

     • At periapsis: distance from Earth’s centre is smallest; speed is greatest in the ideal two-body model.

     • At apoapsis: distance is greatest; speed is smallest in the ideal two-body model.

     • Between them: the satellite moves outward after periapsis, slows down, passes apoapsis, then moves
     inward and speeds up.

     Why? Gravity continually changes the satellite’s velocity. In an elliptical orbit, the satellite trades kinetic
     energy (motion) and gravitational potential energy (position). Near Earth it moves faster; farther away it
     moves slower. It is not an engine accelerating it at periapsis.

       For a perfectly circular orbit, distance and orbital speed are constant. There is no unique closest or
       farthest point, so periapsis-based angle descriptions become undefined or convention-dependent.

     A simple lap
     Picture a clock hand travelling around an oval. Put 0° at the closest point. Half a lap later, at 180°, it reaches
     the farthest point. The angle is measured at Earth’s centre, in the plane of the orbit—not from the ground and
     not from north on a map.

     That angle is true anomaly, written ν (Greek letter nu).

     4. True anomaly — the “you are here” angle

True anomaly answers one focused question: “From the closest point of this ellipse, what angle around
     the orbit has the satellite travelled?”

     True anomaly                       Meaning for an elliptical orbit

     0°                                 At periapsis — closest point.

     Between 0° and 180°                On the outbound half, moving away from periapsis toward apoapsis.

     180°                               At apoapsis — farthest point.

     Between 180° and 360°              On the inbound half, moving from apoapsis back toward periapsis.

     360° (same as 0°)                  Back at periapsis after one full revolution.

     How does a tracker know the true anomaly?
     A tracker does not usually watch the satellite and measure this angle directly with a protractor. It estimates
     the satellite’s orbit from observations or uses an orbit model supplied as orbital elements. Given the orbit and
     the reference time, the software calculates where the satellite should be now. From that calculated position, it
     can determine true anomaly.

     1. Obtain the orbit description and its reference epoch (the time the elements apply to).

     2. Advance the satellite’s position from that epoch to the time you want.

     3. Find the satellite’s position in the orbital plane.

     4. Measure the angle from periapsis to that position: that is true anomaly.

     In common public tracking systems, the input may be a TLE (two-line element set). A TLE does not normally
     list true anomaly as a continuously updated live reading. It supplies parameters for a propagation model; the
     software computes the current position and related quantities.

     Why true anomaly alone is not enough
     Suppose two satellites both have ν = 90°. That means each is one-quarter of the way in angular position from
     periapsis, but it does not mean they are above the same place on Earth. Their orbit sizes, shapes,
     inclinations, plane orientations, periapsis directions, and reference times may differ.

       Remember: true anomaly is a position angle inside the orbit. Latitude/longitude are locations on
       Earth’s surface. They are different coordinate ideas.

     5. Argument of periapsis — pointing to the closest
     point
     The argument of periapsis, ω (omega), tells you where periapsis lies within the orbital plane. First RAAN
     orients the plane in space. Then ω tells you how the ellipse is turned inside that plane.

     A useful sequence is:

     1. Inclination: how much the orbital plane is tilted relative to the equator.

     2. RAAN: where that plane crosses the equatorial plane in the chosen reference direction.

     3. Argument of periapsis: from the ascending-node direction, measure within the orbital plane to periapsis.

     The ascending node is where the satellite crosses the equatorial plane going from south to north. The
     descending node is the crossing going north to south.

ω does not directly tell you the maximum speed by itself. Speed is greatest at periapsis for an elliptical orbit,
     but the value of ω tells you the direction of periapsis within the plane. Whether that point is over the Northern
     or Southern Hemisphere depends on the full geometry—including inclination and the orientation of the plane.
     So “ω = 90° means northern” is not a universal rule without a stated reference geometry.

     6. Mean motion — the orbit’s rhythm
     Mean motion, commonly written n, is the average angular rate of orbital motion. Tracking data often
     expresses it as the number of revolutions per day. It is closely tied to the semi-major axis: for an ideal
     two-body orbit, a larger orbit has a longer period and fewer revolutions per day.

     Use this relationship as a mental model:

       Smaller orbit → shorter period → more laps per day.
       Larger orbit → longer period → fewer laps per day.

     For an Earth satellite in a low orbit, a typical period might be around 90–100 minutes, corresponding to
     roughly 14–16 revolutions per day. The International Space Station is roughly in this range; its exact orbit
     changes.

     A geostationary satellite is a special case: it circles Earth once per sidereal day (about 23 hours 56 minutes),
     in a circular equatorial orbit and in Earth’s rotation direction. Its mean motion is therefore about 1.0027
     revolutions per 24-hour solar day—not exactly 1.0000 if the unit is revolutions per 24 hours.

     Mean motion is not one of the six classical elements
     The six elements are usually a, e, i, Ω, ω, and a position-at-epoch quantity (often true anomaly, mean
     anomaly, or another equivalent representation). Mean motion is normally derived from the orbit size under the
     model being used. It is very useful in tracking displays and TLEs, but it is not an extra independent seventh
     element.

     A caution about circular orbits
     When an orbit is circular, the closest point is not unique. A system may use a different angular reference,
     such as argument of latitude, to describe position. So do not force periapsis and true anomaly onto every
     circular-orbit display.

     7. The ground track — why the line shifts on the map
     A ground track is the path made by the point on Earth directly beneath the satellite (the sub-satellite point). It
     is not the orbit drawn in deep space. A map is attached to Earth, and Earth rotates while the satellite moves.

     Imagine a satellite completing one orbit in 90 minutes. During those 90 minutes, Earth rotates eastward by
     about:

     360° × (90 minutes ÷ 1,440 minutes per day) = 22.5°

     That simple calculation explains why the next pass does not trace exactly the same longitude path on a map.
     In a typical prograde low-Earth orbit, the ground track appears shifted west on the next orbit because Earth
     has rotated east underneath the orbital plane.

       Important wording: the orbital plane is approximately fixed in inertial space over a short interval,
       while Earth rotates beneath it. Real orbital planes can slowly precess due to Earth’s non-spherical
       gravity, so “perfectly locked in space” is a useful short-term simplification, not a universal long-term
       truth.

Do not confuse three different lines
     • Orbit in space: the satellite’s three-dimensional path around Earth.

     • Ground track: the moving footprint directly below the satellite, drawn on an Earth-fixed map.

     • Visibility footprint: the wider area from which a satellite may be visible or a sensor may observe; it
     depends on altitude, geometry, antenna or sensor limits, and other conditions.

     A satellite can pass over the same broad region on different orbits, but the ground track may be offset. A
     sun-synchronous orbit is designed so its orbital plane precesses at a rate that keeps the local solar time of its
     passes approximately consistent; that is a separate effect from Earth’s daily rotation.

     8. Reading a tracking display without getting lost
     Suppose a tracking display gives you these example values. Treat them as a teaching example, not as the
     live state of a particular satellite.

     Display item                            How to read it

     Semi-major axis / altitude              Orbit size and approximate distance from Earth. Altitude is measured above the surface;
                                             semi-major axis is measured from Earth’s centre.

     Eccentricity                            How circular or stretched the orbit is.

     Inclination                             How tilted the orbital plane is relative to Earth’s equator.

     RAAN                                    Which direction the orbital plane is oriented around Earth’s polar axis, relative to a
                                             reference direction.

     Argument of periapsis                   Where the closest point sits inside the orbital plane.

     True anomaly / current position         Where the satellite is along the ellipse at the stated time.

     Period / mean motion                    How long one orbit takes / how many orbits happen per day.

     Latitude / longitude / altitude         The satellite’s computed current geographic position and height, if shown.

     Next AOS / LOS                          For a ground station, approximate acquisition of signal and loss of signal; depends on
                                             station location and visibility limits.

     A practical order for looking at the screen
     1. Check the time: every computed position is tied to a particular moment.

     2. Check the orbit: size, shape, tilt, and plane orientation.

     3. Check position along the orbit: current position or anomaly.

     4. Check the output you actually need: map position, next ground-station pass, coverage, or contact window.

     5. Check the source and age of the orbital data. An old element set can make predictions less accurate,
     especially for low satellites affected by drag.

     9. Five common traps
     Trap 1: “The first four are fixed forever.”
     Better: they are useful as slowly changing orbit landmarks over a short interval. Real orbits are perturbed, and
     some elements can change appreciably depending on the orbit and timescale.

Trap 2: “True anomaly is the only thing that changes.”
     Better: true anomaly describes the current angular position in the ideal orbit. Time and computed geographic
     coordinates also change, and real orbital elements can evolve.

     Trap 3: “Mean motion of 1.0 always means geostationary.”
     Better: it depends on the unit and orbit geometry. Geostationary requires an equatorial, circular, prograde
     orbit with a period matching Earth’s sidereal rotation. A rounded display may show about one revolution per
     day.

     Trap 4: “ω = 90° always means periapsis is in the north.”
     Better: ω is measured from the ascending-node direction within the orbital plane. Hemisphere depends on the
     full orientation and reference convention.

     Trap 5: “The ground track is the orbit.”
     Better: the ground track is the projection of the satellite’s position onto rotating Earth. The orbital path exists
     in three dimensions.

     10. Quick self-check
     1. You know a, e, i, and Ω. Which two classical elements still describe the ellipse’s periapsis direction and the
        satellite’s position?

     2. At what true anomaly is the satellite at apoapsis in an elliptical orbit?

     3. If a satellite’s period becomes shorter, does mean motion generally increase or decrease?

     4. Why does the next ground track shift relative to the previous one?

     5. Does a true anomaly of 90° identify one unique point on Earth for every satellite?

     6. Why is a geostationary satellite’s period tied to a sidereal day rather than exactly 24 hours?

     Answers — check only after trying
     1. Argument of periapsis (ω) and true anomaly (ν), or an equivalent position-at-epoch parameter.

     2. 180°.

     3. Increase: more revolutions occur in a given day.

     4. Earth rotates eastward under the orbital plane; the ground track is Earth-fixed.

     5. No. It is an angle in that satellite’s own orbital geometry, not a global latitude/longitude.

     6. A geostationary satellite must match Earth’s rotation relative to the stars, which is one sidereal day.

     11. The one-minute mental model
       SIZE tells you how large the orbit is.
       SHAPE tells you how stretched it is.
       TILT tells you the angle of the orbital plane to the equator.
       TWIST (RAAN) orients that plane around Earth’s axis.
       ω tells you where periapsis lies inside the plane.
       ν tells you where the satellite is along the orbit at this moment.

     Then keep two useful supporting ideas in mind:

• Mean motion / period: the orbit’s rhythm—how many laps per day or how long each lap takes.

     • Ground track: where the satellite’s sub-satellite point travels across the rotating Earth.

     You do not need to memorise every formula before using a tracker. First learn to ask the right question of
     each field. Once the picture is clear, formulas and software outputs become much easier to interpret.

     A short practice routine (10 minutes)
     1. Open any orbit viewer and choose one satellite.

     2. Find the orbit period or mean motion. Estimate how many laps it makes in a day.

     3. Find inclination. Say aloud what it means without using the word “inclination.”

     4. Look at its ground track and compare two consecutive passes.

     5. If the software exposes orbital elements, identify ω and ν; explain in one sentence why they answer
     different questions.

     End of guide. Keep this sentence: the elements describe the orbit and the satellite’s place in it at a given
     time; the ground track shows that motion on a rotating Earth.
