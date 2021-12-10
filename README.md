# AVPE
Anime.js Vue Particle Explosion

Prop | Type | Default | Function
--- | --- | --- | --- |
amount | Number | 100 | Amount of particles per emit.
borderRadiusStart | Number | 0 | Sets the border-radius property on the particle at the start.
borderRadiusEnd | Number | 1px | Sets the border-radius of the particle at the end.
colorStart | String | #FF0000 | Starting color, do not use literal values like 'red'.
colorEnd | String | #000000 | Ending color, do not use literal values like 'blue'.
duration | Number | 500 | Duration of particle explosion animation, in ms.
ease | String | easeInBounce | Ease function. (https://easings.net/)
opacityStart | Number | 1 | Opacity to start the particles at.
opacityEnd | Number | 0 | Opacity to end the particles with.
radius | Number | 50 | Radius of particle explosion.
sizeStart | String | 2px | Size of the particle, use CSS sizing, '2px' for example.
sizeEnd | String | 1px | Size of the particle, use CSS sizing, '1px' for example.
zindex | Number | -1 | Sets the z-index of the particles so you can place them behind values.

Here is an example of what it does via a component, which has a slot so you can add content.
![AVPE Example](AVPE_example.gif)
