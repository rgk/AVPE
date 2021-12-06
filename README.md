# AVPE
Anime.js Vue Particle Explosion

Prop | Type | Function
--- | --- | --- |
amount | Number | Amount of particles per emit.
color | String | Starting color, do not use literal values like 'red'.
colorEnd | String | Ending color, do not use literal values like 'blue'.
duration | Number | Duration of particle explosion animation, in ms.
ease | String | Ease function. (https://easings.net/)
size | String | Size of the particle, use CSS sizing, 2px for example.
radius | Number | Radius of particle explosion.

Here is an example of what it does via a component, which has a slot so you can add content.
![AVPE Example](AVPE_example.gif)
