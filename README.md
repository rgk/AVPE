# AVPE
Anime.js Vue Particle Explosion

![AVPE Example](AVPE_example.gif)

Prop | Type | Default | Function
--- | --- | --- | --- |
amount | Number | 100 | Amount of particles per emit.
borderRadiusStart | Number | 0 | Sets the border-radius property on the particle at the start.
borderRadiusEnd | Number | "1px" | Sets the border-radius of the particle at the end.
colorStart | String | "random" | Starting color, do not use literal values like 'red', has 'random' option.
colorEnd | String | "random" | Ending color, do not use literal values like 'blue', has 'random' option.
durationMax | Number | 500 | Duration of animation, max value if durationMin is set, in ms.
durationMin | Number | durationMax | Minimum duration of animation, defaults to the value of durationMax, in ms.
ease | String | "easeInBounce" | Main ease function. (https://easings.net/)
easeBorderRadius | String | ease | Specific ease function for borderRadius.
easeHeight | String | ease | Specific ease function for height.
easeWidth | String | ease | Specific ease function for width.
easeOpacity | String | ease | Specific ease function for opacity.
opacityStart | Number | 1 | Opacity to start the particles at.
opacityEnd | Number | 0 | Opacity to end the particles with.
radius | Number | 50 | Radius of particle explosion.
rotateMin | Number | 0 | The minimum rotate amount in degrees, can be negative.
rotateMax | Number | 0 | The maximum rotate amount in degrees, can be negative.
sizeWidthStart | String | "2px" | Start width of the particle, use CSS sizing, '2px' for example.
sizeHeightStart | String | sizeWidthStart | Start height of the particle, use CSS sizing, '2px' for example.
sizeWidthEnd | String | "1px" | End width of the particle, use CSS sizing, '1px' for example.
sizeHeightEnd | String | sizeWidthEnd | End height of the particle, use CSS sizing, '1px' for example.
zindex | Number | -1 | Sets the z-index of the particles so you can place them behind values.

Here is an example of what it does via a component, which has a slot so you can add content.
