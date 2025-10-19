# A Memory's A Heavy Burden

## Challenge Description
You now find yourself in the place where many climbers have been laid to rest. A cold wind moves through the temple grounds, carrying whispers of the departed. Stone lanterns and marble graves reflect Buddhist traditions, their shadows stretching across the frost-covered earth.

The temple rests in the shadow of a very iconic mountain, quiet and imposing. Every detail in the image, the arrangement of the graves, the lanterns, and the lingering scent of incense, holds clues to its true location. You need to uncover the exact coordinates of where you are to move on from here.

Note: round off coordinates to 3 decimal places.

`Flag format: citadel{XX.XXX_XXX.XXX}`


## Solve
**Flag:** `citadel{35.486_138.699}`

In this challenge, we download an image which shows a grave with a mountain in the background.
- Looking at the picture, with the mountain in the background and shrines and also the challenge mentions *Buddhist*, so the first identification of the mountain seems to be *Mt. Fuji* in Japan.
- Also, we see a compass at the bottom which says *South*. Therefore, the Temple/Shrine is located somewhere **North** of *Mt. Fuji*.
- On the google maps, we search for *Temple* and shortlist the ones which lie  north to *Mt. Fuji*.
- Going to street view of each of them eventaully gives us the correct location.
- We get exact coordinates as `-35.485689`, `138.698744`. Rounding off to 3 decimal places, we get our flag.