Decision : Can we ensure that aviation flight data (airline, route, departure, arrival, status) is correctly structured and validated before it is stored, shared, or analyzed?
Signals:
1 Flight Identification → Each <flight> has a required <flightNumber> (e.g., “AI101”), which uniquely identifies the record.
2 Airline Integrity → <airline> is mandatory, ensuring that every flight is tied to an operator.
3 Route Coverage → <route> must contain <departure> and <arrival> airports, ensuring completeness.
4 Time Tracking → Departure/arrival timestamps (in your XML) capture schedule accuracy.
5 Flight Status → <status> tag ensures every record has operational state (e.g., “On Time”, “Delayed”).
6 Validation Test → sample.xml passes because all required fields are present and in correct order.
7 Error Example → broken.xml fails because it omits <status>, violating the DTD constraint.
Gaps:The DTD does not enforce airport codes format (e.g., “LAX”, “SFO”), so typos like “XXZ” could still pass.
     No validation of date/time format (e.g., “2025-08-31T10:00” vs “10:00 AM”).
     Cannot enforce uniqueness of flight numbers (duplicates are possible).
Risk:If Wrong: Invalid XML could allow flights without status or missing routes → miscommunication in aviation systems.
     If Stale: Schema not updated with new required fields (like gate or terminal) could cause data loss.
     Operational Harm: Incorrect flight data could affect schedules, passenger updates, and airline compliance reporting.
Stewardship:Who sees it: Internal airline IT teams, aviation analysts, and system integrators.
            How long kept: At least 1 year (aligned with aviation record-keeping standards).
            Visibility: Shared only inside aviation operations and data engineering teams (not customer-facing).
Data Domain : Primary -> Aviation Flight Tracking Data.
              Adjacent Domains -> Travel & Ticketing Systems (passenger booking, check-in).
                                  Transportation Logistics (cargo flights, connections with ports).
