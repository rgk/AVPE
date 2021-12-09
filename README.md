# AVPE
Anime.js Vue Particle Explosion

Prop | Type | Function
--- | --- | --- |
amount | Number | Amount of particles per emit.
borderRadius | Number | Sets the CSS border-radius property on the particles so you can make them round.
color | String | Starting color, do not use literal values like 'red'.
colorEnd | String | Ending color, do not use literal values like 'blue'.
duration | Number | Duration of particle explosion animation, in ms.
ease | String | Ease function. (https://easings.net/)
size | String | Size of the particle, use CSS sizing, 2px for example.
radius | Number | Radius of particle explosion.
startingOpacity | Number | Opacity to start the particles at.
endingOpacity | Number | Opacity to end the particles with.

Here is an example of what it does via a component, which has a slot so you can add content.
![AVPE Example](AVPE_example.gif)
