# flood
A web app for flood risk assessment

## Conceptual Model
Assume that a city in a low-land area (large square) where water is flooding over its infrastructure (small squared).         
<img src="https://kietpawpan.github.io/flood/flood.jpg" width="300" height="300">

The thickness of the water layer is called flood height (H), which equals the volume of flood water (V) divided by the city area (A). However, the water has been partially replaced by the volume of infrastructure under flood water (Vi). Hence,

```
let V = 4000 * 1000000; // cubic meter
let A = 5000 * 1000000; // squared meter
let H = (V+Vi)/A;

```


## Credits
Image by Gemini: https://lh3.googleusercontent.com/gg/ACM6BIvx4gTOyCjSHr-Z4-vxKMiXyebZf1YFJd_M9927JYjz7ZTXN1hAUqCY-nQ28x0TQqQs2nDT0LXo3qQwvUj5bfzZgQvNtlDitkkEEQirbPUmNHlhml1Vf4ZSIHUdFn9EqkTywhpLTi116AFGZo7rL-GRQwRqLT9n8IAc6TBR8rXmX0fd9Ks
