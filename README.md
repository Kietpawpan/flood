# Flood Dynamics and Risk Assessment
Bangkok remains vulnerable to flooding, and the risk is likely to increase in the future due to climate change. Therefore, ongoing efforts are needed to improve flood prevention and response capabilities. 
 
This repository offers a [web application](https://kietpawpan.github.io/flood/flood.html) designed to evaluate flood risk in Bangkok under the worst-case scenario of seawater intrusion.

## Theoretical Formulation
In urban areas, such as Bangkok, flooding often manifests as a sheet of water inundating both land and infrastructure:         

|<img src="https://kietpawpan.github.io/flood/flood.jpg" width="300" height="300">
|:--:| 
| *Urban flooding model* |

The thickness of the water layer, known as flood height (H), is calculated by dividing the volume of floodwater (V) by the city's area (A). However, this calculation can be adjusted to account for the volume of infrastructure submerged beneath the floodwater (Vi), which can partially displace the water.

Below is the JavaScript code for evaluating flood risk in Bangkok based on a specified critical flood height.

```
function flood() {
  // Get input values
  const expectedFloodHeight = document.getElementById("H").value;
  const infrastructureAreaFraction = document.getElementById("F").value;
  const infrastructureHeight = document.getElementById("h").value;
  const canalWidth = document.getElementById("Wc").value;
  const canalDepth = document.getElementById("Dc").value;
  const canalWaterFraction = document.getElementById("Vt").value;
  const waterFlowRate = document.getElementById("fr").value;



  // Calculate areas and volumes-Only the infrastructure beneath foodwater is considered
  var infrastructureVolume = "";
  const bangkokArea = 1568.7 * 10000000;
  const infrastructureArea = bangkokArea * infrastructureAreaFraction;
    if(infrastructureHeight<expectedFloodHeight){infrastructureVolume = infrastructureArea * infrastructureHeight;}
    else{infrastructureVolume = infrastructureArea * expectedFloodHeight;}
  const canalLength = 2604 * 1000;
  const canalVolume = canalLength * canalWidth * canalDepth;
  const canalWaterVolume = canalVolume * canalWaterFraction;
  const waterVolume = (bangkokArea * expectedFloodHeight) - infrastructureVolume + canalWaterVolume;

  // Calculate hazard quotient
  const dailyWaterVolume = waterFlowRate * 60 * 60 * 24;
  const hazardQuotient = dailyWaterVolume / waterVolume;

  // Display results
  document.getElementById("Vw").innerHTML = waterVolume.toLocaleString() + " m<sup>3</sup>";
  document.getElementById("V").innerHTML = dailyWaterVolume.toLocaleString() + " m<sup>3</sup>/day.";
  document.getElementById("hq").innerHTML = hazardQuotient.toFixed(1);
  document.getElementById("head").innerHTML = "Discussion";

  // Determine flood risk
  if (hazardQuotient < 0.5) {
    // Negligible risk
    document.getElementById("hq").style.color = "green";
    document.getElementById("dis").innerHTML = "Bangkok is at negligible risk of flooding. The actual water volume is less than what's needed to reach the " + expectedFloodHeight + " meters flood height.";
  } else if (hazardQuotient < 1) {
    // Low risk
    document.getElementById("hq").style.color = "yellow";
    document.getElementById("dis").innerHTML = "Bangkok is at low risk of flooding. The actual water volume is less than what's needed to reach the " + expectedFloodHeight + " meters flood height.";
  } else {
    // High risk
    document.getElementById("hq").style.color = "red";
    document.getElementById("dis").innerHTML = "Bangkok is at high risk of flooding. The actual water volume exceeds what's needed to reach the " + expectedFloodHeight + " meters flood height.";
  }
}
```
Therefore, a smaller volume of floodwater is needed to produce the same flood height in areas with infrastructure that can displace water.
## Variables and Parameters
1. __Critical flood height__ (H) is the flood level above which pedestrians or drivers cannot escape safely.
2. __Water flow rate__ (Q) is the quantity of water flowing into the city (m<sup>3</sup>/s.
3. __Duration__ is the times since the flood water is greater than the water draining rate (consecutive days).
4. __Actutal water volume__ is the mass of flood water, which equal inflow - outflow (m<sup>3</sup>. If the inflow is less than the outflow, then the actual water volume is zero.  

## Risk Assessment
The hazard quotient is a useful metric for quantifying flood risk. Here's a breakdown of the concept:

### Hazard Quotient (HQ)
__Formula:__ HQ = Actual Water Volume / Water Volume Causing Flood Height of x Meters

__Interpretation:__
- HQ < 0.5: The area is at low risk of flooding. The actual water volume is less than what's needed to reach the specified flood height.
- 0.5 < HQ < 1: The area is at moderate risk of flooding. The actual water volume is equal to what's needed to reach the specified flood height.
- HQ >= 1: The area is at high risk of flooding. The actual water volume exceeds what's needed to reach the specified flood height.

__Key Considerations__
- x Meters: The chosen flood height is crucial. It should be based on historical data, local infrastructure, and the community's vulnerability to flooding.
- Water Volume: Accurate estimation of both actual and potential water volumes is essential. This involves factors like rainfall intensity, catchment area, and drainage efficiency.
- Flood Risk Mapping: Hazard quotients can be used to create flood risk maps, visually representing areas with different levels of vulnerability.

__Example:__
If a region has an HQ of 0.8 for a flood height of 2 meters, it suggests that the current water volume is 80% of what's needed to cause a 2-meter flood. This indicates a relatively low risk.


## Credits
Figure was created with Gemini.
