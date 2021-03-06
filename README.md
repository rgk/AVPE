# AVPE
Anime.js Vue Particle Explosion

![AVPE Example](AVPE_example.gif)

Prop | Type | Default | Function
--- | --- | --- | --- |
amountMax | Number | 100 | Minimum amount of particles to emit.
amountMin | Number | amountMax | Minimum amount of particles to emit.
blendMode | String | "overlay" | Sets the blend mode of the particles.
borderRadiusStart | Number | 0 | Sets the border-radius property on the particle at the start.
borderRadiusEnd | Number | "1px" | Sets the border-radius of the particle at the end.
boxShadow | String | "0 0 2px rgba(255, 255, 255, 0.123)" | Sets the CSS box-shadow property on the particles.
colorStart | String | "random" | Starting color, do not use literal values like 'red', has 'random' option.
colorEnd | String | "random" | Ending color, do not use literal values like 'blue', has 'random' option.
config | Object | {} | An Anime.js config which will be merged with the default.
defaults | Boolean | TRUE | Use default options, which can still be overwritten by config options.
durationMax | Number | 500 | Duration of animation, max value if durationMin is set, in ms.
durationMin | Number | durationMax | Minimum duration of animation, defaults to the value of durationMax, in ms.
ease | String | "easeInBounce" | Main ease function. (https://easings.net/)
easeBackgroundColor | String | ease | Specific ease function for backgroundColor.
easeBorderRadius | String | ease | Specific ease function for borderRadius.
easeFilter | String | ease | Specific ease function for filters.
easeHeight | String | ease | Specific ease function for height.
easeWidth | String | ease | Specific ease function for width.
easeOpacity | String | ease | Specific ease function for opacity.
easeRotate | String | ease | Specific ease function for rotate.
easeX | String | ease | Specific ease function for translateX.
easeY | String | ease | Specific ease function for translateY.
filterStart | String | "blur(1px)" | CSS filter value(s) for the start of the effect, make sure they match filterEnd.
filterEnd | String | "blur(0px)" | CSS filter value(s) for the end of the effect, make sure they match filterStart.
opacityStart | Number | 1 | Opacity to start the particles at.
opacityEnd | Number | 0 | Opacity to end the particles with.
radiusMax | Number | 50 | Maximum radius of particle explosion.
radiusMin | Number | radiusMax | Minimum radius of particle explosion.
rotateMax | Number | 0 | The maximum rotate amount in degrees, can be negative.
rotateMin | Number | rotateMax * -1 | The minimum rotate amount in degrees, can be negative.
sizeWidthStart | String | "2px" | Start width of the particle, use CSS sizing, '2px' for example.
sizeHeightStart | String | sizeWidthStart | Start height of the particle, use CSS sizing, '2px' for example.
sizeWidthEnd | String | "1px" | End width of the particle, use CSS sizing, '1px' for example.
sizeHeightEnd | String | sizeWidthEnd | End height of the particle, use CSS sizing, '1px' for example.
zindex | Number | -1 | Sets the z-index of the particles so you can place them behind values.
