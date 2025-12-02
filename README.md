# RatGuard-NYC

THE PROBLEM

New York City faces a persistent rat infestation that is most visible around trash-collection areas, subway entrances, and commercial zones. Rats multiply quickly and carry health risks, especially at night when trash bags accumulate. This problem affects public health, urban sanitation, and the overall quality of life.

WHO IT AFFECTS

>Local residents

>Restaurant workers & owners

>Commuters

>Sanitation workers

>Public health officials

SOLUTION OVERVIEW


A camera-based detection system that uses existing NYC street and subway cameras to identify rat activity and alert users before an infestation grows.

ARCHITECTURE OVERVIEW
Inputs

These values come from two sources:
(1) AI analysis of city cameras, and
(2) user/environment data.

detectedRats (int)

Provided by a computer-vision module analyzing live camera footage.

isNightTime (bool)

trashLevel (int, 0–100)

>Trash Level	Meaning
>0–30	Clean area
>30–60	Moderate trash
>60–80	High trash accumulation
>80–100	Overflowing trash

userReportedSightings (int)

trapActivations (int) — optional, from physical smart traps

Outputs

Rat Risk Level: LOW / MEDIUM / HIGH

Recommended actions:

“Secure trash immediately.”

“Alert sanitation services.”

“Monitor area during nighttime hours.”

Data Needed (C++ Variables)
int detectedRats;
bool isNightTime;
int trashLevel;
int userReportedSightings;
int trapActivations;
string ratRiskLevel;

3. Core Logic (Pseudocode)
START

INPUT detectedRats
INPUT isNightTime
INPUT trashLevel
INPUT userReportedSightings
INPUT trapActivations

SET ratRiskLevel = "LOW"

// CAMERA-BASED DETECTION
IF detectedRats >= 1 AND detectedRats <= 3 THEN
    ratRiskLevel = "MEDIUM"
END IF

IF detectedRats > 3 THEN
    ratRiskLevel = "HIGH"
END IF

// NIGHTTIME MULTIPLIER
IF isNightTime == TRUE AND detectedRats > 0 THEN
    ratRiskLevel = "HIGH"
END IF

// TRASH CONDITIONS
IF trashLevel > 70 THEN
    ratRiskLevel = "MEDIUM"
END IF

IF trashLevel > 80 AND isNightTime == TRUE THEN
    ratRiskLevel = "HIGH"
END IF

// USER REPORTS
IF userReportedSightings >= 3 THEN
    ratRiskLevel = "HIGH"
END IF

// SMART TRAP DATA
IF trapActivations > 2 THEN
    ratRiskLevel = "HIGH"
END IF

// OUTPUT RESULTS
OUTPUT "Rat Risk Level: " + ratRiskLevel

IF ratRiskLevel == "HIGH" THEN
    OUTPUT "ACTION: Secure trash immediately."
    OUTPUT "ACTION: Notify sanitation services."
ELSE IF ratRiskLevel == "MEDIUM" THEN
    OUTPUT "ACTION: Monitor area and clean surroundings."
ELSE
    OUTPUT "ACTION: No action needed."
END IF

END

4. C++ Connection

The system relies on existing NYC cameras (traffic, public-safety, and MTA cameras). These cameras are not modified physically.
Instead, a separate AI module analyzes their video feed and sends a simple integer to our C++ logic:

detectedRats = 0, 1, 2, 3...


This keeps the project realistic and within the scope of C++ fundamentals.

Mapping to C++:

IF/ELSE statements map to regular C++ conditional blocks.

while(true) loops can be used if the system checks repeatedly.

Inputs come through cin or simulated functions.

Outputs are printed using cout.

Example:

if (detectedRats > 3) {
    ratRiskLevel = "HIGH";
}


All AI/video processing is outside the C++ portion — C++ only receives numerical or boolean signals and reacts accordingly.
