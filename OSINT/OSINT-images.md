---
title: "Imange and Location OSINT"
permalink: /OSINT-image/
layout: single
author-profile: true
---

## Reverse image search
- Google Image Search - https://images.google.com
- Yandex - https://yandex.com
- TinEye - https://tineye.com

- Google: drag image in image search. 
- Yandex: best for image search, 
- Tineye: upload photo and see if it brings anything different

## Viewing EXIF Data

http://exif.regex.info/exif.cgi

Used to be very insecure but companies are using better techniques to hide EXIF data now.  
Record location, device data, date/time.

## Physical Location OSINT

- Go to google and to to address.
- Look at satellite view
- Look for doors, guards, cameras, ways in, places to park to fly a drone from.
- Identifying Geographical Locations
- GeoGuessr - https://www.geoguessr.com
- GeoGuessr - The Top Tips, Tricks and Techniques - https://somerandomstuff1.wordpress.com/2019/02/08/geoguessr-the-top-tips-tricks-and-techniques/

## Geoguessr tips

- Applies to Location OSINT using images.
- Blurry images are usually USA or australia and more remote areas of the country
- If the sun looks in the northern hemisphere then you're probably in the southern hemisphere.and vise versa  (red end of compass is north)
- If shadow point south your probably in southern hemisphere
- If the sun is directly overhead your likely between the tropic of capricorn and the tropic of cancer
- If a satellite dish points south your likely in the northern hemisphere and vise versa
- Countries of British origin and most island countries (not canada, philippines or iceland). Most other countries drive on the right.
- If there's no cars around look for signposts
- Look for car indicators like antenna or wing mirrors to determine car's direction
- Only the USA, UK and liberia and myanmar use miles for speed limit.
- Also can determine road direction by what side of the car the steering wheel is on
- If the middle of the road has yellow lines then you're likely in one of the america continents with the exception of the country chile. South Africa and Japan have the occasional yellow line. Faded yellow line is usually mexico or south america
- Dashed white lines on the edges of roads are quite common in the countries of Denmark, Norway, Iceland and Sweden. 
- Norway tends to have yellow centre lines and Sweden tends to have white centre lines.
- Finland often has centre yellow lines and centre white dashed lines; it doesn’t have dashed lines on the edges of its roads. 
- Russia has a road line that is thinner than other country’s road lines.
- Denmark usually have very short dashed lines
- The four countries of South Africa, Botswana, Eswatini and Lesotho tend to have simultaneous yellow edge road lines and white road centre lines for their major roads.
- Richer the country better the roads
- Russia usually have crumbing roads
- Europe roads tend to be narrower than american roads
- Russia /Ukraine usually have black and white guardrails. Rest of Europe is usually silver.
- Rumble strips is usually in america/canada


## Image and Location Tools

sudo apt install libimage-exiftool-perl exiftool <img>

Use on images to get locations
