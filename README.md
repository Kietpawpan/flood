# Flood Dynamics and Risk Assessment
 Bangkok remains vulnerable to flooding, and the risk is likely to increase in the future due to climate change. Therefore, ongoing efforts are needed to improve flood prevention and response capabilities. Here, this repository provides a [web application](https://kietpawpan.github.io/flood/flood.html) for assessing risk associated with flood dynamics in Bangkok. 

## Theoretical Formulation
1. In rural areas, where the predominant land use is agriculture, flooding often manifests as a layer of water covering the land (__Fig.1__).

|<img src="https://kietpawpan.github.io/flood/flood0.jpg" width="300" height="300">
|:--:| 
| *__Fig.1__ Rural flooding model* | 

2. In urban areas, such as Bangkok, flooding often manifests as a sheet of water inundating both land and infrastructure. (__Fig.2__).         

|<img src="https://kietpawpan.github.io/flood/flood.jpg" width="300" height="300">
|:--:| 
| *__Fig.2__ Urban flooding model* |

The thickness of the water layer, known as flood height (H), is calculated by dividing the volume of floodwater (V) by the city's area (A). However, this calculation can be adjusted to account for the volume of infrastructure submerged beneath the floodwater (Vi), which can partially displace the water:

```
function flood(){

let H = document.getElementById("H").value; // Expected flood height of x meters

let F = document.getElementById("F").value; // Fraction of infrastructure area in the city

let h = document.getElementById("h").value; // height of infra

if(h>H){h=H;} // count only the infra height under water
else{;}

let a = 1568.7 * 10000000 * F; // area of infrastructures

let area = 1568.7 * 10000000; // Bangkok

let Lc = 2604 * 1000; // Canals length (m)

let Wc = document.getElementById("Wc").value; // canal width

let Dc = document.getElementById("Dc").value; // canal depth

let Vt = document.getElementById("Vt").value; // fraction of water volume alraedy in canal

let Vc = Lc * Wc * Dc;

let Vi = a * h; // infra volume

let Vf = Vc * Vt; // canal volume * fraction of space in canal

let Vw = (area * H) - Vi + Vf;  // water volume casing flood height of x meter

var flow = document.getElementById("fr").value;

var volume = flow * 60 * 60 * 24; // squared meter per day of actual water

var hq = volume/Vw; // hazard quotient

let Result = Vw.toLocaleString();

document.getElementById("Vw").innerHTML = Result + " m<sup>3</sup>";
document.getElementById("V").innerHTML = volume.toLocaleString() + " m<sup>3</sup>/day.";
document.getElementById("hq").innerHTML = hq.toFixed(1);
document.getElementById("head").innerHTML = "Discussion";

if(hq<0.5){document.getElementById("hq").style.color="green";
document.getElementById("dis").innerHTML = "Bangkok is <font color='green'><b>at negligible risk of flooding</b></font>. The actual water volume is less than what's needed to reach the <font color='green'><b>" + H +  " meters </b></font> flood height.";}

else if(hq<1){document.getElementById("hq").style.color="yellow";
document.getElementById("dis").innerHTML = "Bangkok is <font color='yellow'><b>at low risk of flooding</b></font>. The actual water volume is less than what's needed to reach the <font color='yellow'><b>" + H +  " meters </b></font>flood height.";}

else if(hq>=1){document.getElementById("hq").style.color="red";
document.getElementById("dis").innerHTML = "Bangkok is <font color='red'><b>at high risk of flooding</b></font>. The actual water volume exceeds what's needed to reach the <font color='red'><b>" + H +  " meters </b></font>flood height.";}

}

```
Therefore, a smaller volume of floodwater is needed to produce the same flood height in areas with infrastructure that can displace water.

## Risk Assessment
The hazard quotient is a useful metric for quantifying flood risk. Here's a breakdown of the concept:

### Hazard Quotient (HQ)
__Formula:__ HQ = Actual Water Volume / Water Volume Causing Flood Height of x Meters

__Interpretation:__
- HQ < 1: The area is at low risk of flooding. The actual water volume is less than what's needed to reach the specified flood height.
- HQ = 1: The area is at moderate risk of flooding. The actual water volume is equal to what's needed to reach the specified flood height.
- HQ > 1: The area is at high risk of flooding. The actual water volume exceeds what's needed to reach the specified flood height.

__Key Considerations__
- x Meters: The chosen flood height is crucial. It should be based on historical data, local infrastructure, and the community's vulnerability to flooding.
- Water Volume: Accurate estimation of both actual and potential water volumes is essential. This involves factors like rainfall intensity, catchment area, and drainage efficiency.
- Flood Risk Mapping: Hazard quotients can be used to create flood risk maps, visually representing areas with different levels of vulnerability.

__Example:__
If a region has an HQ of 0.8 for a flood height of 2 meters, it suggests that the current water volume is 80% of what's needed to cause a 2-meter flood. This indicates a relatively low risk.


## Credits
Figures 1 and 2 are powered by Gemini.
