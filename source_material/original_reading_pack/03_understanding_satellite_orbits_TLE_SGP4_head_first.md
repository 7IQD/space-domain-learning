# Understanding Satellite Orbits, TLE and SGP4

> Reading order: 03 of 05  
> Purpose: Follow the chain from tracking observations to orbit determination, TLE, SGP4 and predicted satellite state.

**Original PDF:** `03_understanding_satellite_orbits_TLE_SGP4_head_first.pdf`

---

UNDERSTANDING SATELLITE
                       ORBITS,
                    TLE AND SGP4
                       A Head First Concept Note for a Technical Layman

  Purpose
  Build a connected mental model of how tracking observations lead to an estimated orbit, how a TLE
  represents that estimate, and how SGP4 predicts satellite position and velocity at a requested time.

  The central chain
    Tracking observations → Orbit determination → TLE → SGP4 → Predicted position
    and velocity → Earth-fixed location

    Begin with the problem, understand each piece, then connect the complete
                                    process.

1. The problem we are trying to solve
  Suppose we want to know where a satellite will be at 10:30 tomorrow morning. Its current position is
  not enough because it is moving continuously around Earth.

  We need to describe the orbit's size and shape, its orientation around Earth, where the satellite was
  along that orbit at a known time, and how its motion evolves with time.

  Tracking observations help estimate these details. The estimated orbital information can be
  represented in a standard format called a Two-Line Element set (TLE). A mathematical model called
  SGP4 uses the TLE to predict the satellite's position and velocity at a requested time.

    Tracking observations → Orbit estimation → TLE → SGP4 → Predicted position and
    velocity

  2. First, imagine a satellite moving around Earth
  Imagine Earth as a ball and the satellite moving along a path around it. That path is the satellite's
  orbit. To describe it, we need to answer three different questions:

   Question                                               What we need to describe

   How big is the orbit, and what is its shape?           Orbit size and eccentricity

   How is the orbit tilted and oriented around Earth?     Inclination, RAAN and argument of perigee

   Where is the satellite at a particular time?           Anomaly and time information

  These are different questions. One orbital parameter cannot answer all three.

  3. Start with the simplest possible orbit
  Imagine a perfectly circular orbit. For this simplified example, suppose the orbital radius is 7,000 km
  and the satellite takes 90 minutes to complete one revolution. We temporarily ignore the
  complications of a real orbit.

  To describe the satellite's position in this two-dimensional example, we need two things:

   • Radius: how far the satellite is from the centre.

   • Angle: how far around the circle it has travelled from a chosen starting direction.

  The radius tells us distance; the angle tells us direction. Together they identify the position in the
  orbital plane.

  What about velocity?
  Velocity tells us both how fast the satellite is moving and in which direction. In circular motion, the
  instantaneous direction of motion is tangent to the circle—the direction the path is heading at that
  point.

    Position tells us where the satellite is. Velocity tells us how it is moving at that
    instant.

4. Why do we need six orbital parameters?
  Real satellite orbits are generally not perfect circles, and they do not all lie in the same plane. Six
  classical orbital elements are commonly used to describe the orbit's size, shape, orientation and the
  satellite's progress along it.

  A. Semi-major axis — how large is the orbit?
  For an ellipse, imagine drawing the longest line through its centre. The semi-major axis, represented
  by a, is half the length of that line. It describes the overall size of the ellipse. For a circular orbit, it
  equals the orbital radius.
  Question answered: How large is the orbit?

  B. Eccentricity — how circular or stretched is the orbit?
  Eccentricity, represented by e, describes orbit shape. A value of 0 is a perfect circle; a value above 0
  and below 1 describes an ellipse. An ellipse has a closest point to Earth called perigee and a farthest
  point called apogee. In a circular orbit there is no unique closest or farthest point.
  Question answered: What is the shape of the orbit?

  C. Inclination — how much is the orbit tilted?
  Imagine Earth's equator as a flat sheet passing through Earth's centre: this is the equatorial plane.
  Imagine another flat sheet containing the satellite's orbit: this is the orbital plane. The angle
  between these two planes is inclination, represented by i. At 0°, the orbit lies in the equatorial plane;
  at 90°, the planes are perpendicular.
  Question answered: How much is the orbital plane tilted relative to Earth's equatorial plane?

  D. RAAN — where is the orbital plane oriented around Earth?
  The orbital plane intersects Earth's equatorial plane along a line called the line of nodes. The two
  crossing points are the ascending node (south-to-north crossing) and descending node
  (north-to-south crossing).

  RAAN means Right Ascension of the Ascending Node. It specifies the angular direction of the
  ascending node, measured in the equatorial reference plane from a defined reference direction.

    Think of the distinction this way: inclination tells us how much the plane is tilted;
    RAAN tells us in which direction that tilted plane is oriented around Earth. RAAN
    does not tell us where the satellite is along its orbit.

  E. Argument of perigee — where is the closest point within that
  plane?
  The argument of perigee, represented by ω (omega), measures the angle in the orbital plane from
  the ascending node to perigee, in the direction of orbital motion. It tells us how the ellipse is
  oriented within its plane. For a circular orbit, perigee is not uniquely defined, so this angle has no
  unique physical meaning by itself.

  F. Anomaly — where is the satellite along the orbit?
  We know the orbit's size, shape and orientation, but the satellite is moving. We need to know its
  position along the orbit at a particular time. Two anomaly terms matter here: mean anomaly and
  true anomaly.

5. Mean anomaly versus true anomaly
  True anomaly
  Imagine standing at Earth's centre and drawing one line to perigee and another to the satellite's
  current position. The angle between these lines, measured in the direction of orbital motion, is the
  true anomaly, represented by ν (nu). It is the satellite's actual angular position relative to perigee.

   • At perigee, true anomaly is 0°.

   • At apogee, true anomaly is 180°.

  Mean anomaly
  Mean anomaly, represented by M, is a mathematical measure of average orbital progress. In the
  basic orbital model, it advances uniformly with elapsed time. It is not the satellite's actual geometric
  angle.

  Why are they different?
  A satellite moves faster near perigee and slower near apogee in an elliptical orbit. Its actual angular
  progress therefore does not match the uniform progress represented by mean anomaly.

   Mean anomaly (M)                                                True anomaly (ν)

   Uniform mathematical measure of progress                        Actual angular position relative to perigee

   Advances uniformly with time in the basic model                 Changes at a non-uniform rate in an elliptical orbit

   Included in a standard TLE                                      Not directly supplied as a standard TLE orbital element

    For a circular orbit, they coincide when measured from the same reference
    direction. For an elliptical orbit, they generally differ.

  6. Where does time enter the calculation?
  Knowing the orbit is not enough. Two satellites can share the same orbit but be on opposite sides of
  Earth. We need a time reference and information about orbital progress at that time.

  Epoch — the reference time
  The epoch is the date and time associated with the TLE's orbital elements. It is a time tag, not an
  angle, a point on the orbit, or the satellite's position itself.

  Mean anomaly at epoch — the reference progress
  The TLE contains a mean anomaly associated with that epoch. Together, epoch and mean anomaly
  establish the reference progress along the orbit.

  Mean motion — how quickly the satellite goes around
  Mean motion is usually expressed in revolutions per day. For example, 15.5 revolutions per day
  corresponds to an approximate orbital period of 1440 ÷ 15.5 ≈ 92.9 minutes. This is an approximate
  period, not a guarantee that every real revolution takes exactly that long.

   Term                          Its role

   Epoch                         When the orbital information is referenced

   Mean anomaly                  Reference orbital progress

   Mean motion                   Average orbital revolution rate

7. What is a TLE, really?
  TLE means Two-Line Element set. It is a standard text format containing estimated orbital
  information for a satellite. It is not a table of positions at every minute.

  A TLE contains satellite identification, epoch, inclination, RAAN, eccentricity, argument of perigee,
  mean anomaly, mean motion and additional fields used by the format and propagation model. It
  does not list all six classical orbital elements in exactly the same form; for example, it provides
  mean motion rather than directly listing semi-major axis.

  Where does a TLE come from?
   • Tracking systems obtain observations of the satellite.

   • Orbit determination uses those observations to estimate an orbit.

   • The estimated orbital information is represented in TLE format.

   • A propagation model uses the TLE to predict the satellite's state at other times.
    Orbit determination estimates the orbit from observations. Propagation predicts
    the satellite's state using the estimated orbit.

  A TLE is an estimate, not a guarantee of the exact position. Prediction accuracy depends on the
  quality and age of the TLE and how the real satellite's motion differs from the model.

  8. What does SGP4 do?
  SGP4 stands for Simplified General Perturbations 4. For our purpose, think of it as the mathematical
  model designed to propagate a satellite's orbit from TLE data.

  SGP4 takes a TLE and a requested calculation time. It returns predicted position and velocity
  together as the satellite's state vector.

  Does SGP4 first draw the orbit?
  No. SGP4 can calculate the state directly at a requested time. If you want positions every minute,
  you ask SGP4 to calculate the state at each of those times and then plot the positions to display the
  orbit.

  Does SGP4 simply move the satellite around an ellipse at constant
  speed?
  No. SGP4 uses a prescribed set of mathematical equations and corrections to model orbital motion,
  including important perturbation effects within the model. It is a propagation model, not merely a
  drawing tool.

  9. What exactly is a state vector?
  A state vector describes the satellite's motion at one particular time. It consists of six numbers:

   • Position: x, y, z.

   • Velocity: vx, vy, vz.

  The position components describe where the satellite is relative to a defined origin and coordinate
  axes. The velocity components describe how its position is changing along those axes. The
  coordinate frame matters: the same physical satellite can have different numerical coordinates in
  different reference frames.
  Illustrative values only: position = (1000, 2000, 3000) km; velocity = (2, 5, −1) km/s. These are not a real satellite
  prediction.

Is velocity simply measured from tracking observations and split into
  components?
  Not in the prediction step. Tracking observations help orbit determination estimate the orbital
  information. SGP4 then calculates predicted position and velocity at the requested time. The velocity
  components are outputs of that propagation calculation, not merely a previously measured velocity
  divided into three numbers.

10. Why do we need coordinate systems?
  To state a satellite's position numerically, we must define the origin, the directions of the three
  coordinate axes, and the reference frame in which the coordinates are expressed. This is a
  coordinate frame.

  Orbital-plane coordinates
  We can first describe position and velocity using axes in the plane of the orbit. This is convenient for
  understanding the ellipse and motion along it. But these coordinates are tied to that orbital plane;
  they are not yet expressed along a common set of Earth-centred reference axes.

  Connecting orbital geometry to three dimensions
   • Argument of perigee: establishes the ellipse's orientation within the orbital plane relative to the
     ascending node.

   • Inclination: tilts the orbital plane relative to the equatorial plane.

   • RAAN: establishes the ascending node's direction in the equatorial reference plane.

  These are geometric rotations. The same orientation must be applied consistently to position and
  velocity. This explains why the three orientation parameters are needed: they connect local orbital
  geometry to a common three-dimensional reference frame. This is a conceptual description, not the
  complete sequence of SGP4's internal equations.

  11. What is TEME, and why does SGP4 use it?
  SGP4's standard output is expressed in a reference frame called TEME, short for True Equator, Mean
  Equinox. You do not need to memorise the name first. Understand its purpose: TEME is an
  Earth-centred reference frame with defined axis directions, providing a consistent reference for
  predicted position and velocity.

  TEME coordinates are not latitude, longitude and altitude. TEME is not an Earth-fixed frame. To
  calculate a ground location, the satellite's position must be transformed into an Earth-fixed frame
  using consistent time and reference-frame conventions.

    TEME position and velocity → Earth-fixed coordinates → geodetic latitude, longitude
    and altitude

  This transformation is not merely relabelling the same three numbers. It accounts for the
  relationship between the SGP4 reference frame and Earth's rotating surface. The exact frame
  transformations are a separate topic and should be understood before implementation.

  12. From predicted position to ground track
  A satellite's ground track is the path formed by projecting its position onto Earth's surface. To
  produce one:

   • Choose a sequence of times.

   • Calculate the satellite's position at each time using SGP4.

   • Transform each position into Earth-fixed coordinates.

   • Convert each position into latitude and longitude.

   • Plot those locations on a map.

  The ground track is the surface path directly beneath the satellite, not its physical orbit around
  Earth. Because Earth rotates while the satellite moves, successive ground-track passes generally
  appear at different longitudes.

13. The complete chain — with the purpose of every
  step
   Step                 Input                      What happens                        Output / purpose

   1. Tracking          Measurements or            Observations are collected          Evidence about satellite motion
                        observations

   2. Orbit             Tracking observations      An orbit is estimated               Estimated orbital information
   determination        and an estimation
                        method

   3. TLE creation      Estimated orbital          Information is represented in TLE   TLE with epoch and orbital
                        information                format                              elements

   4. Choose            TLE and requested time     Compare requested time with         Time reference for propagation
   prediction time                                 epoch

   5. SGP4              TLE and requested time     Propagate using SGP4                Predicted position and velocity in
   propagation                                                                         TEME

   6. Frame             TEME state and             Convert to Earth-fixed frame        Coordinates referenced to
   transformation       time/frame conventions                                         rotating Earth

   7. Ground            Earth-fixed position and   Calculate geodetic coordinates      Latitude, longitude and altitude
   location             Earth model

   8. Ground track      Locations at successive    Plot or analyse motion over         Ground track, visibility and
                        times                      Earth's surface                     potential contact windows

  The distinction between steps 2 and 5 is especially important.
    Orbit determination estimates an orbit from observations. SGP4 propagates the
    estimated orbit to predict a state at a requested time.

  Likewise, the TLE epoch is a time reference, not the time at which the satellite's orbit is first drawn.

  14. Five questions that test the mental model
  Answer these before moving to detailed mathematics.

  1. If inclination tells us how much the orbital plane is tilted, what additional information does RAAN
  provide?

  2. What is the difference between the epoch and mean anomaly at epoch?

  3. Why do mean anomaly and true anomaly generally differ in an elliptical orbit?

  4. Does SGP4 need to draw the entire orbit before calculating the satellite's position and velocity at
  a requested time?

  5. Why can't we treat SGP4's TEME coordinates as latitude and longitude directly?

  15. Final mental picture
   • Orbit size and shape describe the path's geometry.

   • Inclination, RAAN and argument of perigee describe how that path is oriented in three dimensions.

   • Mean anomaly, mean motion and epoch provide information about orbital progress and its timing.

   • The TLE packages estimated orbital information in a standard format.

   • SGP4 uses the TLE and requested time to calculate predicted position and velocity.

   • TEME defines the reference frame for SGP4's output.

• Coordinate transformation connects that output to an Earth-fixed reference.

   • Latitude, longitude and altitude express the satellite's location in familiar geographic terms.

  The central idea
    First estimate the orbit from observations. Then use a propagation model to
    predict where the satellite will be and how it will be moving at a specified time.
    Finally, transform the predicted position into the coordinate system needed for the
    application.
