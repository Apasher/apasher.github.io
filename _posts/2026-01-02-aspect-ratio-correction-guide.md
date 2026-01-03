# “Your aspect ratio is wrong”  
## A guide to aspect ratio correction for retro console games by Apasher

Before we begin, I want to preface that there are three different types of aspect ratio, and it is important to know the difference between all three in order to understand how to do proper aspect ratio correction.

**Pixel Aspect Ratio (PAR):** The proportion of pixels in an image. Square pixels are 1:1, but game consoles don’t always output square pixels. We will get to that later.

**Display Aspect Ratio (DAR):** The proportion of the target screen display. For the context of retro consoles, you will only need to know the DAR of a standard definition CRT TV, which is 4:3. However, I will also be using DAR to refer to the proportions of a game's active graphics when displayed on a CRT TV.

**Storage Aspect Ratio (SAR):** The relationship between the width and height of a video frame. For example, the SAR of a 256x224 video frame is 8:7. The SAR of a 320x240 video frame is 4:3. For the most part; if the SAR of a game is not 4:3 or doesn’t match the console’s PAR, it is safe to ignore it.

When it comes to aspect ratios for retro console games, it’s important to keep in mind that before the era of HDMI, they were designed to be displayed on analog consumer CRT TVs. To understand how DAR works on a CRT TV, it's important to keep in mind that the horizontal resolution does not mean how many pixels wide the image is. It wasn't until digital displays came along where horizontal resolution was interpreted as how many pixels wide an image is. CRT displays, on the other hand, do not have pixels. They instead display lines, as a literal electron beam from the back of a vacuum tube is drawing the image line by line. So instead of how many pixels wide the image is, the horizontal resolution determines **how many samples are drawn per line.** So even though a game’s resolution may output 512x224 or 640x240, they are still displayed in a 4:3 frame because it’s the video signal’s **dot clock rate** that determines how the DAR gets corrected on a CRT TV.

There are two different camps that people often take when it comes to aspect ratio correction: one is to keep pixels square to have their game capture as sharp as possible, and the other is to have an accurate representation of what you see on a CRT TV. As mentioned before, most retro game consoles do not output square pixels. However when a game’s SAR matches with the console’s PAR, you get square pixels. Pin Eight has a page documenting the [dot clock frequencies of each console](https://pineight.com/mw/page/Dot_clock_rates.xhtml), with calculations of their PAR included. To give an example: most SNES games internally render in a resolution of 256x224, which gives a SAR of 8:7. And according to Pin Eight, the SNES’s dot clock frequency is 5.37MHz. When dividing Rec 601’s square pixel clock rate of 6.14 MHz for 240p (13.5 MHz * 10/11 /2) by the SNES dot clock frequency, this equates to a PAR of 1.143:1, or 8:7. So displaying a game in an integer scale of 256x224 in your game capture will give you square pixels. Easy, right? Well here’s where things get complicated. When you look at a game-by-game basis, you will notice that some SNES games had their geometry designed for square pixels, while other games accounted for how a CRT TV interpolates the image to a 4:3 frame. And when you get to later consoles like the GameCube, you will notice that the games were not designed to be viewed with square pixels at all. The point is: for some games, capturing in square pixels is perfectly valid. But for some other games, you will not have the intended geometry by capturing in square pixels. So you will have to judge by a game-by-game case whether square pixels are appropriate or not.

So what if you want your game capture to accurately represent what you see on a CRT TV? Well you just stretch it to 4:3 and call it a day, right? After all, that’s what actual CRT TVs do. They interpolate the image to 4:3, so that’s what I should do right? Well, that’s something that most people get wrong. Most people like to crop out the black borders surrounding the image, and then stretch the active game graphics to 4:3. While it is a convenient way to correct aspect ratio, it’s actually not accurate to what you see on a CRT. **It’s not just the active game graphics that get interpolated to 4:3 on a CRT TV. It’s the active game graphics <span style="text-decoration:underline;">plus</span> overscan padding.** So how do you get the correct CRT-accurate aspect ratio in your game capture? Simple, [FirebrandX](https://www.firebrandx.com/) came up with an easy formula that involves taking the horizontal resolution of a game, and multiplying it by the console’s PAR. Alternatively; you can multiply the vertical resolution by the PAR's reciprocal so you can overscan into a standard 4:3 frame, and for consoles that follow the Rec. 601 standard (ie. the GameCube and Wii,) you don’t have to do any calculation whatsoever. You can just capture the 720x480 frame, crop the center to 704x480, and scale it to 4:3. Ste from [HD Retrovision](https://www.hdretrovision.com/) has a [more complex formula](https://cdn.retrorgb.com/wp-content/uploads/2019/02/horiz_correction_factor.png), but for this guide we will be sticking with the FirebrandX formula. Do keep in mind that just like presenting games in square pixels, whether the in-game geometry will look correct or not will completely depend on the game. There are cases where if a game’s SAR is 4:3, that it’s actually desirable to retain its 4:3 aspect ratio, even if it’s not what you see on a CRT. From here on out, I will be giving details for each console on how to correct the aspect ratio for their perspective games. 

Disclaimer: This guide will mainly be focused on NTSC, but I will update this page with complete information for PAL in the future.

# NES/SNES

## <span style="text-decoration:underline;">256px Games</span>

**Resolution (NTSC):** 256x224  
**Storage Aspect Ratio (SAR):** 8:7  
**Pixel Aspect Ratio (PAR):** 8:7  
**4:3-adjusted DAR:** 256 * (8/7) = <span style="text-decoration:underline;">292x224 (73:56)</span>


**Resolution (NTSC):** 256x240  
**Storage Aspect Ratio (SAR):** 16:15  
**Pixel Aspect Ratio (PAR):** 8:7  
**4:3-adjusted DAR (NTSC):** 256 * (8/7) = <u>292x240 (73:60)</u>  

## <span style="text-decoration:underline;">512px Games</span>

**Resolution (NTSC):** 512x224  
**Storage Aspect Ratio (SAR):** 16:7  
**Pixel Aspect Ratio (PAR):** 4:7  
**4:3-adjusted DAR:** 512 * (4/7) = <span style="text-decoration:underline;">292x224 (73:56)</span>  

**Resolution (NTSC):** 512x240  
**Storage Aspect Ratio (SAR):** 32:15  
**Pixel Aspect Ratio (PAR):** 4:7  
**4:3-adjusted DAR:** 512 * (4/7) =** **<span style="text-decoration:underline;">292x240 (73:60)</span>  

# Sega Master System

**Resolution (NTSC):** 256x192  
**Storage Aspect Ratio (SAR):** 4:3  
**Pixel Aspect Ratio (PAR):** 8:7  
**4:3-adjusted DAR:** 256 * (8/7) = <span style="text-decoration:underline;">292x192 (73:48)</span>  

# PC-Engine/TurboGrafx-16

**Resolution (NTSC):** 256x240  
**Storage Aspect Ratio (SAR):** 16:15  
**Pixel Aspect Ratio (PAR):** 8:7  
**4:3-adjusted DAR (NTSC):** 256 * (8/7) = <span style="text-decoration:underline;">292x240 (73:60)</span>  

# Sega Genesis

## <span style="text-decoration:underline;">256px Games</span>

**Resolution (NTSC):** 256x224  
**Storage Aspect Ratio (SAR):** 8:7 (NTSC)
**Pixel Aspect Ratio (PAR):** 8:7  
**4:3-adjusted DAR (NTSC):** 256 * (8/7) = <span style="text-decoration:underline;">292x224 (73:56) </span>  

## <span style="text-decoration:underline;">320px Games</span>

**Resolution (NTSC):** 320x224  
**Storage Aspect Ratio (SAR):** 10:7 (NTSC)
**Pixel Aspect Ratio (PAR):** 32:25  
**4:3-adjusted DAR (NTSC):** 320 * (32/25) = <span style="text-decoration:underline;">292x224 (73:56)</span>  

# Neo Geo AES

**Resolution (NTSC):** 320x240  
**Storage Aspect Ratio (SAR):** 4:3  
**Pixel Aspect Ratio (PAR):** 65:64  
**4:3-adjusted DAR (NTSC):** 320 * (65/64) = <span style="text-decoration:underline;">325x240 (65:48)</span>  

# PlayStation 1

Now we get to the console generation with games that run in various different resolutions. The PlayStation 1 has different dot clock rates for different horizontal resolution modes, and therefore result in different PARs which I will be listing below. The PS1 also has games that can output in 480i, but for the most part the 480i PAR is similar to their 240p counterparts. So if a game outputs 640x480i, the PAR is similar to a 320x240p game. Refer to [this list](https://junkerhq.net/xrgb/index.php?title=Playstation) to check your game’s resolution.

## <span style="text-decoration:underline;">256px Games</span>

**Resolution (NTSC):** 256x240  
**Storage Aspect Ratio (SAR):** 16:15  
**Pixel Aspect Ratio (PAR):** 8:7  
**4:3-adjusted DAR (NTSC):** 256 * (8/7) =** **<span style="text-decoration:underline;">292x240 (73:60)</span>  

## <span style="text-decoration:underline;">320px Games</span>

**Resolution (NTSC):** 320x240  
**Storage Aspect Ratio (SAR):** 4:3  
**Pixel Aspect Ratio (PAR):** 32:25  
**4:3-adjusted DAR (NTSC):** 320 * (32/25) = <span style="text-decoration:underline;">292x240 (73:60)</span>  

## <span style="text-decoration:underline;">384px Games</span>

**Resolution (NTSC):** 384x240  
**Storage Aspect Ratio (SAR):** 16:10  
**Pixel Aspect Ratio (PAR):** 4:5  
**4:3-adjusted DAR (NTSC):** 384 * (4/5) = <span style="text-decoration:underline;">308x240 (77:60)</span>  

## <span style="text-decoration:underline;">512px Games</span>

### Progressive
**Resolution (NTSC):** 512x240  
**Storage Aspect Ratio (SAR):** 32:15  
**Pixel Aspect Ratio (PAR):** 4:7  
**4:3-adjusted DAR (NTSC):** 512 * (4/7) = <span style="text-decoration:underline;">292x240 (73:60)</span>  

### Interlaced
**Resolution (NTSC):** 512x480i  
**Storage Aspect Ratio (SAR):** 16:15  
**Pixel Aspect Ratio (PAR):** 8:7  
**4:3-adjusted DAR (NTSC):** 512 * (8/7) = <span style="text-decoration:underline;">584x480i (73:60)</span>  

## <span style="text-decoration:underline;">640px Games</span>

### Progressive
**Resolution (NTSC):** 640x240  
**Storage Aspect Ratio (SAR):** 8:3  
**Pixel Aspect Ratio (PAR):** 16:35  
**4:3-adjusted DAR (NTSC):** 640 * (16/35) = <span style="text-decoration:underline;">292x240 (73:60)</span>  

### Interlaced
**Resolution (NTSC):** 640x480i  
**Storage Aspect Ratio (SAR):** 4:3  
**Pixel Aspect Ratio (PAR):** 32:25  
**4:3-adjusted DAR (NTSC):** 640 * (32/25) = <span style="text-decoration:underline;">584x480i (73:60)</span>  

# Sega Saturn

The Saturn works differently from the PS1, in that it has the same dot clock rate regardless of a game’s horizontal resolution, with the exceptions being 640px games and 704px games. The Saturn has a “low-res” dot clock (7.16MHz @ 320px/352px), and a “high res” dot clock (14.3MHz @ 640px/704px). So regardless if a game is 320px wide or 352px wide, the PAR will still be the same.

## <span style="text-decoration:underline;">320px Games</span>

**Resolution (NTSC):** 320x224  
**Storage Aspect Ratio (SAR):** 10:7  
**Pixel Aspect Ratio (PAR):** 6:7  
**4:3-adjusted DAR (NTSC):** 320 * (6/7) = <span style="text-decoration:underline;">274x224 (137:112)</span>  

**Resolution (NTSC):** 320x240  
**Storage Aspect Ratio (SAR):** 4:3  
**Pixel Aspect Ratio (PAR):** 6:7  
**4:3-adjusted DAR (NTSC):** 320 * (6/7) = <span style="text-decoration:underline;">274x240 (137:120)</span>  

## <span style="text-decoration:underline;">352px Games</span>

**Resolution (NTSC):** 352x224  
**Storage Aspect Ratio (SAR):** 11:7   
**Pixel Aspect Ratio (PAR):** 6:7  
**4:3-adjusted DAR (NTSC):** 352 * (6/7) = <span style="text-decoration:underline;">302x224 (151:112)</span>  

**Resolution (NTSC):** 352x240  
**Storage Aspect Ratio (SAR):** 22:15 (NTSC), 11:8 (PAL)  
**Pixel Aspect Ratio (PAR):** 6:7  
**4:3-adjusted DAR (NTSC):** 352 * (6/7) = <span style="text-decoration:underline;">302x240 (151:120)</span>  

## <span style="text-decoration:underline;">640px Games</span>

### Progressive
**Resolution (NTSC):** 640x224  
**Storage Aspect Ratio (SAR):** 20:7  
**Pixel Aspect Ratio (PAR):** 3:7  
**4:3-adjusted DAR (NTSC):** 640 * (3/7) = <span style="text-decoration:underline;">274x224 (137:112)</span>  

**Resolution (NTSC):** 640x240  
**Storage Aspect Ratio (SAR):** 8:3  
**Pixel Aspect Ratio (PAR):** 3:7  
**4:3-adjusted DAR (NTSC):** 640 * (3/7) = <span style="text-decoration:underline;">274x240 (137:120)</span>  

### Interlaced
**Resolution (NTSC):** 640x448i  
**Storage Aspect Ratio (SAR):** 10:7 (NTSC)  
**Pixel Aspect Ratio (PAR):** 6:7  
**4:3-adjusted DAR (NTSC):** 640 * (6/7) = <span style="text-decoration:underline;">548x448 (137:112)</span>  

**Resolution (NTSC):** 640x480i  
**Storage Aspect Ratio (SAR):** 4:3  
**Pixel Aspect Ratio (PAR):** 6:7  
**4:3-adjusted DAR (NTSC):** 640 * (6/7) = <span style="text-decoration:underline;">548x480 (137:120)</span>  

## <span style="text-decoration:underline;">704px Games</span>

### Progressive  
**Resolution (NTSC):** 704x224  
**Storage Aspect Ratio (SAR):** 22:7  
**Pixel Aspect Ratio (PAR):** 3:7  
**4:3-adjusted DAR (NTSC):** 704 * (3/7) = <span style="text-decoration:underline;">302x224 (151:112)</span>  

**Resolution (NTSC):** 704x240  
**Storage Aspect Ratio (SAR):** 44:15  
**Pixel Aspect Ratio (PAR):** 3:7  
**4:3-adjusted DAR (NTSC):** 704 * (3/7) = <span style="text-decoration:underline;">302x240 (151:120)</span>  

### Interlaced  
**Resolution (NTSC):** 704x448i  
**Storage Aspect Ratio (SAR):** 11:7  
**Pixel Aspect Ratio (PAR):** 6:7  
**4:3-adjusted DAR (NTSC):** 704 * (6/7) = <span style="text-decoration:underline;">604x448 (151:112)</span>  

**Resolution (NTSC):** 704x480i  
**Storage Aspect Ratio (SAR):** 22:15  
**Pixel Aspect Ratio (PAR):** 6:7  
**4:3-adjusted DAR (NTSC):** 704 * (6/7) = <span style="text-decoration:underline;">604x480 (151:120)</span>  

# Nintendo 64

## <span style="text-decoration:underline;">320px Games</span>

**Resolution (NTSC):** 320x240  
**Storage Aspect Ratio (SAR):** 4:3  
**Pixel Aspect Ratio (PAR):** 120:119  
**4:3-adjusted DAR (NTSC):** 320 * (120/119) = <span style="text-decoration:underline;">322x240 (161:120)</span>  

## <span style="text-decoration:underline;">640px Games</span>

(more information needed: dot clock @ 640x240)


# GameCube/Wii

Now this is where things get complicated. Both the GameCube and the Wii have games that apply an arbitrary amount of horizontal scaling to their games, giving their library a wide variety of horizontal resolutions. For example, Twilight Princess internally renders in a resolution of 608x448, but its output resolution is 666x448. That’s a resolution with a SAR that is too wide, but remember that the output resolution does not define the aspect ratio that you see on a CRT, as it recognizes the signal as 666 *samples per-line*, not 666 pixels wide. It is also important to note that GameCube and Wii games do not have square pixels, as they follow the Rec. 601 standard and have a dot clock of 13.5 MHz, giving a PAR of 10:11. This is a strong case where GameCube/Wii games aren’t meant to be viewed with square pixels, because the pixels aren’t square in the first place. So some form of aspect ratio correction has to be done when the video signal is digitized, especially with games that have horizontal scaling because digital displays and capture cards interpret the scaled resolution as “666 pixels wide” instead of 666 samples-per-line. TL;DR, **if the SAR of your game is not 4:3, ignore it. It does not define the aspect ratio.** Refer to [this list](https://www.gc-forever.com/wiki/index.php?title=Swiss/Forced_Progressive_Compatibility_List) to check your game’s resolution.

## <span style="text-decoration:underline;">640px Games (Most Common)</span>

**Resolution (NTSC):** 640x448  
**Storage Aspect Ratio (SAR):** 10:7  
**Pixel Aspect Ratio (PAR):** 10:11  
**4:3-adjusted DAR (NTSC):** 640 * (10/11) = <span style="text-decoration:underline;">582x448 (291:224)</span>  

**Resolution (NTSC):** 640x480  
**Storage Aspect Ratio (SAR):** 4:3  
**Pixel Aspect Ratio (PAR):** 10:11  
**4:3-adjusted DAR (NTSC):** 640 * (10/11) = <span style="text-decoration:underline;">582x480 (97:80)</span>  


## <span style="text-decoration:underline;">650px Games (Ex. Tony Hawk’s Pro Skater 4)</span>

**Resolution (NTSC):** 650x448  
**Storage Aspect Ratio (SAR):** 325:224 (NTSC)  
**Pixel Aspect Ratio (PAR):** 10:11  
**4:3-adjusted DAR (NTSC):** 650 * (10/11) = <span style="text-decoration:underline;">590x448 (295:224)</span>   

## <span style="text-decoration:underline;">656px Games (Ex. Prince of Persia: The Two Thrones)</span>

**Resolution (NTSC):** 656x448  
**Storage Aspect Ratio (SAR):** 41:28  
**Pixel Aspect Ratio (PAR):** 10:11  
**4:3-adjusted DAR (NTSC):** 656 * (10/11) = <span style="text-decoration:underline;">596x448 (149:112)</span>  

## <span style="text-decoration:underline;">660px Games (Ex. Super Mario Sunshine, Animal Crossing, Wind Waker)</span>

**Resolution (NTSC):** 660x448  
**Storage Aspect Ratio (SAR):** 165:112  
**Pixel Aspect Ratio (PAR):** 10:11  
**4:3-adjusted DAR (NTSC):** 660 * (10/11) = <span style="text-decoration:underline;">600x448 (75:56)</span>  

**Resolution (NTSC):** 660x464  
**Storage Aspect Ratio (SAR):** 165:116  
**Pixel Aspect Ratio (PAR):** 10:11  
**4:3-adjusted DAR (NTSC):** 660 * (10/11) = <span style="text-decoration:underline;">600x464 (75:58)</span>  

**Resolution (NTSC):** 660x480  
**Storage Aspect Ratio (SAR):** 11:8  
**Pixel Aspect Ratio (PAR):** 10:11  
**4:3-adjusted DAR (NTSC):** 660 * (10/11) = <span style="text-decoration:underline;">600x480 (5:4)</span>  

## <span style="text-decoration:underline;">666px Games (Ex. Double Dash, Twilight Princess)</span>

**Resolution (NTSC):** 666x448  
**Storage Aspect Ratio (SAR):** 333:224  
**Pixel Aspect Ratio (PAR):** 10:11  
**4:3-adjusted DAR (NTSC):** 666 * (10/11) = <span style="text-decoration:underline;">606x448 (303:224)</span>  

## <span style="text-decoration:underline;">704px Games (Ex. Ocarina of Time/Master Quest, Majora’s Mask)</span>

**Resolution (NTSC):** 704x480  
**Storage Aspect Ratio (SAR):** 22:15  
**Pixel Aspect Ratio (PAR):** 10:11  
**4:3-adjusted DAR (NTSC):** 704 * (10/11) = <span style="text-decoration:underline;">640x480 (4:3)</span>  
