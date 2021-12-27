# shipdrivertracker_pi
A simulator for AutoTrackerRaymarine

Using ShipDriverTracker to test AutoTrackerRaymarine from the Desktop with no physical Autopilot:
1. In OpenCPN make a route and activate it.
2. In Shipdriver(Track) right click on the screen and pick "Select Vessel Start Position"
3. In Shipdriver(Track) First "Start",  then set a speed, then select "Auto"
4. In AutoTrackRaymarine select "Tracking" which will set the heading for ShipdriverTrack and actually steer the ship.
5. Next play with it, set a current, activate next waypoint, monitor the reaction. Start from a point off the route etc.

Comments: 
1. It is not AutotrackRaymarine that skips to the next WP, but OpenCPN. AutotrackRaymarine just follows the route to the next active WP.>
2. Why would the ship be so far off the track at various places? Do I have settings that need to be set within AutotrackRaymarine?

At activation (pressing Tracking button) AutotrackRaymarine issues a ZeroXTE command to OpenCPN. At that moment OpenCPN lays out a virtual route segment to the next active waypoint. If that active waypoint is not the first waypoint in the route, it looks as if you are not following the route. But you are following the newly laid out segment to the active waypoint, with a low value of XTE. This is the case in the first image you sent.

The reason I send this ZeroXTE at activation is a matter of user experience. You spot a mark that is on the route (active) and you activate AutotrackRaymarine. That means you expect to go to that mark. Without the ZeroXTE you would first go to the original route segment, then to the active WP. But normally this feels you are going in the wrong direction, the pilot will aggressively steer to the original route segment. Sometimes however you may need to follow the route segment as laid out, in case of obstructions. In that case you better first steer to the route before activating AutotrackRaymarine.

So the first leg of the route is not following the route on the chart, but but leads from the point of activation to the next WP. This is reflected in a low XTE while being off track from the route on the chart.


3. I think AutoTrackRaymarine was trying to compensate for current, but not enough perhaps. (See the XTE along the route in the screenshot.)

You do not need to compensate for currents (you actually can't), this is done automatically by AutotrackRaymarine itself. A current will cause a systematic XTE, this will add to the integrating component of the PID algorithm, causing a systematic correction. It may take a few moments for this correction to build up to the required value. This corresponds to your second picture. In the same way compass errors and drift are corrected.

4. The ship did not stop it just kept going without any further instructions at the end of the route.

At the end of the route the route is deactivated by OpenCPN. AutotrackRaymarine will stop at that moment. It will set the Raymarine pilot to Standby. But not the emulating Shipdriver. You will have to act yourself, just like on a real ship. 


Icons made by Freepik(http://www.freepik.com) from Flaticon(https://www.flaticon.com/) and is licensed by Creative Commons BY 3.0 (http://creativecommons.org/licenses/by/3.0/)
