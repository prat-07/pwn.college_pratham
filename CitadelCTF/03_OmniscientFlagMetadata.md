# Omniscient Flag Metadata

## Challenge Description
As you step into the second chamber, a figure manifests before you. Before you stands a forgotten deity, a dead god spoken of only in whispers. Known by countless names: “Apostle of Epilogue and Eternity,” “Lone Messiah” and many more lost to time.

They leave nothing but a single image, a relic carrying his final secret. Hidden within its layers lies the key to ascend to the next chamber.


## Solve
**Flag:** `citadel{th1s_ch4ll3ng3_1s_f0r_th4t_0ne_ex1ft00l_4nd_b1nw4lk_enthus14st}`

- We are given a link to a pgn file.
- As the challenge talks about metadata, we gather the same using `exiftool`.
- In the author section, we see the message `kdj had a habit of hiding images within images`.
- This clearly means, another image is hidden inside this image. After some research I found that we can use tools like `binwalk` to extract embedded images.
- The flag is written on the image extracted.
