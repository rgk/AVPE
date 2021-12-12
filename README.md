# AVPE
Anime.js Vue Particle Explosion

![AVPE Example](AVPE_example.gif)

Prop | Type | Default | Function
--- | --- | --- | --- |
amount | Number | 100 | Amount of particles per emit.
borderRadiusStart | Number | 0 | Sets the border-radius property on the particle at the start.
borderRadiusEnd | Number | 1px | Sets the border-radius of the particle at the end.
colorStart | String | random | Starting color, do not use literal values like 'red', has 'random' option.
colorEnd | String | random | Ending color, do not use literal values like 'blue', has 'random' option.
duration | Number | 500 | Duration of particle explosion animation, in ms.
ease | String | easeInBounce | Ease function. (https://easings.net/)
opacityStart | Number | 1 | Opacity to start the particles at.
opacityEnd | Number | 0 | Opacity to end the particles with.
radius | Number | 50 | Radius of particle explosion.
rotate | Boolean | true | Enable random rotation of particles from rotateMin to rotateMax.
rotateMin | Number | -360 | The minimum rotate amount.
rotateMax | Number | 360 | The maximum rotate amount.
sizeStart | String | 2px | Size of the particle, use CSS sizing, '2px' for example.
sizeEnd | String | 1px | Size of the particle, use CSS sizing, '1px' for example.
zindex | Number | -1 | Sets the z-index of the particles so you can place them behind values.

Here is an example of what it does via a component, which has a slot so you can add content.
