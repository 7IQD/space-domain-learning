# From Space to Ground Track

> Reading order: 05 of 05  
> Purpose: Consolidate the space-to-ground explanation, including the camera-at-Earth-centre mental model and a solved frame-conversion example.

**Original PDF:** `05_head_first_reference_frames_ground_track.pdf`

---

FROM SPACE TO GROUND TRACK
 A Head First chapter on ECI, TEME, ECEF and latitude–longitude

 The central question: We can calculate a satellite's position in space. How do we use that position to find
 where it is above the rotating Earth?

 The short answer
 We first describe the satellite using axes that do not turn with Earth's daily rotation. Then we describe the same
 physical position using axes attached to Earth. That second description tells us where the satellite is relative to
 places on Earth's surface. We then express the result as latitude and longitude.

 Keep this picture: the satellite keeps moving; Earth keeps rotating; the reference grid is what we change.
 We do not stop either object.

1. Start with the problem
 Imagine observing a satellite from outside Earth. At one instant, it occupies one definite physical point in space. To
 write that point as numbers, we need an origin and three measuring directions (X, Y and Z). These form a
 coordinate reference frame.

 The satellite does not carry one universal set of X, Y and Z numbers. The numbers depend on the measuring grid
 we choose. Change the grid, and the numbers change; the physical satellite position does not.

 Earth rotates while the satellite orbits. If our grid stays oriented in space, Earth's daily rotation is not mixed into the
 grid. This is useful for describing orbital motion. But that grid does not directly tell us the satellite's longitude over
 the rotating Earth.

 For ground location, we need a second grid that turns with Earth. A fixed place on the surface then keeps
 essentially the same coordinates in that grid, while the satellite's coordinates change as it moves overhead.

 2. The two grids
 ECI — Earth-Centred Inertial. ECI is a family of Earth-centred frames whose axes are oriented in space rather
 than rotating with Earth's daily rotation. It is useful for describing orbital motion without the coordinate grid spinning
 with Earth. ECI is a family name; a particular frame and its convention must be specified.

 ECEF — Earth-Centred, Earth-Fixed. Its origin is Earth's centre and its axes rotate with Earth. The grid is
 attached to the rotating Earth, so a fixed ground location keeps essentially constant ECEF coordinates. ECEF is
 useful for describing the satellite relative to Earth's surface.

 Important: ECEF does not make the satellite stationary. The satellite continues along its orbit. ECEF simply
 measures its changing position against an Earth-attached grid.

 3. Where TEME fits
 TEME means True Equator, Mean Equinox. It is a specific Earth-centred, space-oriented reference frame used
 by the standard SGP4 propagation model with TLE data. SGP4 outputs the satellite's position and velocity in
 TEME.

 “True equator” refers to the equatorial plane associated with the true celestial pole at the date in question. “Mean
 equinox” supplies the reference direction in that equatorial plane, using the mean-equinox convention. Together,
 these conventions specify TEME's orientation.

 TEME is not Earth-fixed. It does not rotate with Earth's surface once per day. Also, TEME is not interchangeable
 with every other ECI frame: the exact frame convention matters when converting coordinates.

 Retain this distinction: ECI is the broad family; TEME is one specific frame used by SGP4 with TLEs.

 4. Why change from TEME to ECEF?
 Imagine a longitude line through a ground location and extend its direction into space. That direction rotates with
 Earth. A space-oriented TEME grid does not rotate with that longitude line.

 At a chosen instant, TEME gives the satellite's position against space-oriented axes. To ask “where is it over Earth
 at this instant?”, we must know how Earth is turned relative to those axes at that same instant. We account for
 Earth's rotation and express the same position in ECEF.

 The transformation does not move the satellite. It changes the coordinate description from one grid to
 another. The calculation uses the correct time and frame conventions; it is not merely relabelling X, Y and Z.

 TEME: where is the satellite against space-oriented directions? ECEF: where is that same satellite against
 directions attached to Earth?

5. The camera-at-Earth-centre picture
 Your camera analogy is a useful mental aid. Imagine an imaginary camera at Earth's centre, free to point in any
 direction. At a particular instant, it points along the direction from Earth's centre to the satellite. That direction gives
 the satellite's line of sight from Earth's centre.

 Where that direction meets a simple spherical Earth gives the geocentric sub-satellite point. This is a useful first
 picture of ground projection.

 One refinement: Earth is not a perfect sphere. Real mapping commonly uses an oblate ellipsoid such as WGS-84.
 Software uses the Earth-fixed Cartesian position and the chosen Earth model to calculate geographic latitude,
 longitude and altitude. On an ellipsoid, the exact geodetic sub-satellite point is not always exactly where a straight
 ray from Earth's centre meets the surface.

 Keep the camera picture for intuition; remember that real software uses a defined mathematical Earth model
 for the final geographic coordinates.

 6. From ECEF to latitude and longitude
 ECEF represents the satellite with three Cartesian coordinates (X, Y, Z), measured from Earth's centre along
 Earth-fixed axes. A geographic conversion produces: latitude (north/south), longitude (east/west), and altitude
 (height above the reference ellipsoid).

 A ground track is made by repeating this conversion at successive times and plotting the resulting
 latitude–longitude points. Joining those points shows the path of the satellite's sub-satellite point across the map.

 7. Solved case study: Earth's rotation changes the longitude
 We use a deliberately simple spherical-Earth example. It isolates the reason for changing frames; it is not a full
 SGP4 calculation.

 Given: At one instant, a satellite is above the equator at 7,000 km from Earth's centre. In our space-oriented frame
 its position is (7,000, 0, 0) km. Suppose Earth's zero-longitude direction has rotated 30° eastward relative to that
 space grid.

 Question: What is the satellite's longitude relative to Earth?

 Step 1. The satellite is still at the same physical point. Changing coordinate systems does not move it.

 Step 2. ECEF's X-axis has rotated 30° with Earth's zero-longitude direction. Express the satellite in this new grid
 by rotating its coordinates by −30°:

 XECEF = 7,000 cos(30°) = 6,062 km
 YECEF = −7,000 sin(30°) = −3,500 km
 ZECEF = 0 km

 Step 3. Longitude = atan2(Y, X) = atan2(−3,500, 6,062) = −30°, or 30° west of the ECEF zero-longitude meridian
 under this rotation convention. Latitude is 0° because the satellite lies in the equatorial plane.

 Result: The ground projection is at 0° latitude, 30° west longitude in this simplified example.

 What did we learn? In the space-oriented grid, the satellite coordinates were (7,000, 0, 0). But Earth's longitude
 grid had rotated. In the Earth-fixed grid, the same physical position became (6,062, −3,500, 0). The numbers
 changed because the measuring grid changed. That is why the TEME-to-ECEF step is needed.

8. The complete TLE-to-ground-track story
Stage                          What happens                                                  Why

TLE + requested time           Supply the orbit description and the time for which a         We need an orbit model and a time.
                               position is wanted.

SGP4 → TEME                    SGP4 calculates satellite position and velocity in TEME.      TEME is the frame used by the TLE/SGP4
                                                                                             convention.

TEME → ECEF                    Account for Earth's orientation/rotation and express the      We need the satellite's position relative to
                               same position in Earth-fixed axes.                            the rotating Earth.

ECEF → lat/lon/alt             Convert Earth-fixed Cartesian coordinates using an Earth      We need a geographic location that can be
                               model.                                                        mapped.

Repeat over time               Calculate and plot successive geographic positions.           The sequence of points is the ground track.

 9. Why this matters for operations
 Once the ground track is known, planners can compare it with ground-station locations, regions of interest and
 timing requirements. They can estimate when the satellite will pass within communication range of a ground
 station, or when it will pass over a region to be imaged. The ground track bridges orbit prediction and Earth-based
 operations.

 10. Five points to retain
 1. The satellite has one physical position at a given instant.
 2. Coordinates depend on the reference frame used to describe that position.
 3. ECI is a family of space-oriented, Earth-centred frames; TEME is a specific frame used by SGP4 with TLEs.
 4. ECEF rotates with Earth, so it describes the satellite relative to Earth's surface.
 5. Latitude and longitude are calculated from the Earth-fixed position; repeating them over time gives the ground
 track.

 The final mental picture
 First grid: measure the satellite against directions that stay oriented in space. Second grid: replace that grid
 with one attached to the rotating Earth. The satellite has not jumped or stopped; only the measuring grid has
 changed. The first grid helps describe orbital motion. The second helps find the satellite relative to Earth.

 Technical note
 Real high-accuracy TEME-to-Earth-fixed transformations require a defined time system, Earth-orientation conventions and the
 appropriate rotation model. This chapter uses a simplified conceptual explanation and a spherical-Earth numerical example to clarify the
 purpose of the frame change. It is not a substitute for a validated astrodynamics library or operational orbit-processing procedure.
