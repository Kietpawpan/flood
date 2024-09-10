# Flood Dynamics and Risk Assessment
A web app for assessing risk associated with flood dynamics in Bangkok

## Theoretical Formulation
In rural areas, where there are mainly paddy fields, flooding is a layer of water above the land.

<img src="https://kietpawpan.github.io/flood/flood0.jpg" width="300" height="300">

In urban areas, such as a city in a low-land area, can be viewed as a layer of water (large square) over the land and its infrastructure (small squared).         
<img src="https://kietpawpan.github.io/flood/flood.jpg" width="300" height="300">

The thickness of the water layer is called flood height (H), which equals the volume of flood water (V) divided by the city area (A). However, the water has been partially replaced by the volume of infrastructure under flood water (Vi). Hence,

```
let V = 4000 * 1000000; // cubic meter
let A = 5000 * 1000000; // squared meter
let H = (V+Vi)/A;

```
Thus, there is a smaller volume of flood water to casue the same flood height when there is the infrastructure that replaces the water. 

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
Image by Gemini: 
- https://lh3.googleusercontent.com/gg/ACM6BIvx4gTOyCjSHr-Z4-vxKMiXyebZf1YFJd_M9927JYjz7ZTXN1hAUqCY-nQ28x0TQqQs2nDT0LXo3qQwvUj5bfzZgQvNtlDitkkEEQirbPUmNHlhml1Vf4ZSIHUdFn9EqkTywhpLTi116AFGZo7rL-GRQwRqLT9n8IAc6TBR8rXmX0fd9Ks
- https://lh3.googleusercontent.com/gg/AJIvXiv3h5AKDU4nT6_cG-Lsi_a44EX91-eZ32ePNoTSqFsKF6tiAdOXnkTy4TZ3uv1lXwHkqMq8KA8Xnd2zR8x0tddrz6ZDJaq7-es8NQ9TBhqTJmldHV6V8t77wcM9HjWTLmI4zrjBkMOVGEmDaSDLM4_ha3YvZ2Ntq4zqlT1HIo682iwY2YGV
