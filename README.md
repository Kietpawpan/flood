# Flood Dynamics and Risk Assessment
Bangkok remains vulnerable to flooding, and the risk is likely to increase in the future due to climate change. Therefore, ongoing efforts are needed to improve flood prevention and response capabilities. 
 
This repository offers a [web application](https://kietpawpan.github.io/flood/flood.html) designed to evaluate flood risk in Bangkok under the worst-case scenario of seawater intrusion. The methodology and underlying concepts are detailed in this [article](https://kietpawpan.github.io/flood/floodRisk.pdf).

## Theoretical Formulation
In urban areas, such as Bangkok, flooding often manifests as a sheet of water inundating both land and infrastructure:         

|<img src="https://kietpawpan.github.io/flood/flood.jpg" width="300" height="300">
|:--:| 
| *Urban flooding model*[^1]. |

The thickness of the water layer, known as flood height (H), is calculated by dividing the volume of floodwater (V) by the city's area (A). However, this calculation can be adjusted to account for the volume of infrastructure submerged beneath the floodwater (Vi), which can partially displace the water.

Below is the JavaScript code for evaluating flood risk in Bangkok based on a specified critical flood height.

```
function flood() {
  // Get input values
  const criticalFloodHeight = document.getElementById("H").value;
  const infrastructureAreaFraction = document.getElementById("F").value;
  const infrastructureHeight = document.getElementById("h").value;
  const canalWidth = document.getElementById("Wc").value;
  const canalDepth = document.getElementById("Dc").value;
  const canalWaterFraction = document.getElementById("Vt").value;
  const waterFlowRate = document.getElementById("fr").value;
  const duration = document.getElementById("dur").value;



  // Calculate areas and volumes-Only the infrastructure beneath foodwater is considered
  var infrastructureVolume = "";
  const bangkokArea = 1568.7 * 10000000;
  const infrastructureArea = bangkokArea * infrastructureAreaFraction;
    if(infrastructureHeight<criticalFloodHeight){infrastructureVolume = infrastructureArea * infrastructureHeight;}
    else{infrastructureVolume = infrastructureArea * criticalFloodHeight;}
  const canalLength = 2604 * 1000;
  const canalVolume = canalLength * canalWidth * canalDepth;
  const canalWaterVolume = canalVolume * canalWaterFraction;
  const actualWaterVolume = (bangkokArea * criticalFloodHeight) - infrastructureVolume + canalWaterVolume;

  // Calculate hazard quotient
  var dailyWaterVolume = "";
    if (waterFlowRate < 2198.12){dailyWaterVolume = 0;}
    else{dailyWaterVolume = (waterFlowRate - 2700.06) * 60 * 60 * 24;}
  var hazardQuotient = (dailyWaterVolume * duration) / actualWaterVolume;
  var waterVolumePerDay = dailyWaterVolume / (duration*60*60*24);
  var DailyFloodWater = waterVolumePerDay.toLocaleString();
  document.getElementById("flow3day").innerHTML = DailyFloodWater + " m/s for " + duration + " consecutive days.";

  // Display results
  document.getElementById("Vw").innerHTML = actualWaterVolume.toLocaleString() + " m<sup>3</sup>";
  document.getElementById("V").innerHTML = dailyWaterVolume.toLocaleString() + " m<sup>3</sup>/day.";
  document.getElementById("hq").innerHTML = hazardQuotient.toFixed(1);
  document.getElementById("head").innerHTML = "Discussion";


  // Determine flood risk
  if (hazardQuotient < 0.5) {
    // Low risk
    document.getElementById("hq").style.color = "green";
    document.getElementById("dis").innerHTML = "Bangkok is at low risk of flooding. The actual water volume is less than what's needed to reach the " + criticalFloodHeight + " meters flood height.";
  } else if (hazardQuotient < 1) {
    // Moderate risk
    document.getElementById("hq").style.color = "yellow";
    document.getElementById("dis").innerHTML = "Bangkok is at moderate risk of flooding. The actual water volume is less than what's needed to reach the " + criticalFloodHeight + " meters flood height.";
  } else {
    // High risk
    document.getElementById("hq").style.color = "red";
    document.getElementById("dis").innerHTML = "Bangkok is at high risk of flooding. The actual water volume exceeds what's needed to reach the " + criticalFloodHeight + " meters flood height.";
  }
}

```
Therefore, a smaller volume of floodwater is needed to produce the same flood height in areas with infrastructure that can displace water.
## Variables

1. __Critical Flood Height:__ The maximum water level at which pedestrian or vehicular access becomes hazardous or impossible due to flooding.
2. __Overflow Duration:__ The consecutive number of days during which the flood water level exceeds the capacity of the drainage system.
3. __Water Inflow Rate:__ The volumetric flow rate of water entering the city or region, measured in cubic meters per second (m³/s).
4. __Infrastructure Area Fraction:__ The ratio of the total area occupied by infrastructure (<i>e.g.</i>, buildings, roads) to the total area of the city or region.
5. __Infrastructure Height:__ The height of infrastructure elements (<i>e.g.</i>, buildings) that are submerged during a flood.
6. __Canal Width:__ The width of the canal used to drain flood water from the city to the sea, measured in meters (m).
7. __Canal Depth:__ The depth of the canal used to drain flood water from the city to the sea, measured in meters (m).
8. __Actual Water Volume:__ The net volume of flood water in the city or region, calculated as the difference between the inflow and outflow rates over time. If the outflow rate exceeds the inflow rate, the actual water volume is zero.
9. __Canal Space Fraction:__ The ratio of the empty volume within the canal to the total volume of the canal.

## Parameters Used
1. Bangkok area is 1,568.7 km<sup>2</sup> [^2].
2. The capacity of the drainage system in Bangkok in 2024 is 2,700.06 m<sup>3</sup>/s [^3].
   
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

## Disclaimer:
> [!CAUTION]
> The information provided by this web application is intended for general informational purposes only and should not be construed as professional advice or a substitute for consultation with qualified  professionals. While we strive to provide accurate and up-to-date information, we cannot guarantee the accuracy, completeness, or reliability of the data.   
>
> The application uses a few data sources, including drainage system capacity in Bangkok and Bangkok surface area. These data sources may have limitations or inaccuracies, and the results generated by the application should be interpreted with caution.
> 
> The application does not constitute a guarantee or prediction of future flood events. Users should exercise their own judgment and take appropriate precautions based on the information provided. We are not liable for any damages or losses arising from the use or reliance on the information provided by this application.   
>
> By using this application, you acknowledge and agree to the terms of this disclaimer.

## Reference
[^1]: Image by Gemini.
[^2]: Wikipedia. 2024. Bangkok. https://en.wikipedia.org/wiki/Bangkok
[^3]: Bangkok Drainage and Sewerage Departemment. 2024. Flood Prevention Plan B.E. 2567 (in Thai). p. 2-9. https://dds.bangkok.go.th/public_content/files/001/0008491_1.pdf

