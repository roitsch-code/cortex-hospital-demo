# City Traffic Operations — Konrad-Adenauer-Bridge detour (synthetic demo data)

Owner: City Traffic Control Center (Verkehrsleitzentrale). Classification: internal, city-visible.

## Situation
- Konrad-Adenauer-Bridge closed after a major incident (tram collision, line 66).
- Detour corridor: 24 signalized intersections, 6 of them with emergency-vehicle priority.
- Goal of the Traffic Flow Agent: reduce waiting times and queue length on the detours.

## Allowed data for the Traffic Flow Agent
- Signal timings of the detour intersections (green/red phases, cycle length).
- Aggregated traffic flow from loop detectors (vehicles per minute, queue length).
- Road closures and the official detour plan.
- The agent may PROPOSE signal plans. The City Traffic Control Center applies them.

## Not part of this agent's scope
- Emergency-vehicle priority (green wave) is owned by the Dispatch Center (ILS) and is
  always applied before any optimized signal plan.
- Dispatch incident data, ambulance positions and ambulance routes are not available to
  this agent.

## Detour status (example)
| Intersection | Avg. wait | Queue | Emergency priority |
|---|---|---|---|
| K-01 Reuterbrücke approach | 74 s | 210 m | yes |
| K-02 Ramersdorf ramp | 58 s | 140 m | yes |
| K-03 Südstadt junction | 41 s | 90 m | no |
| K-04 Rheinaue link | 66 s | 175 m | yes |
