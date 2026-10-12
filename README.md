# terradot_baseball
**_This repository displays my most polished app and the decisions I made in production_**

<img width="1280" height="675" alt="Screenshot of Stuff+ & Tunneling Dashboard" src="https://github.com/user-attachments/assets/856e48ab-98ef-4a4f-956d-9de97d2fd132" />

_#Overview_
Pictured above is the Dashboard of my Stuff+ & Tunneling app. This app brings together two prized statistics in the world of pitching.

I was asked to make a tunneling interface and knew that Stuff+ was another huge stat in pitching for many coaches so I decided to merge the two into one app. 

I think that these two statistics can give a coach a good idea of how he can take advantage of all the talents of his pitcher.

_#Data Cleaning_
I first had to clean 30GB of data over 5 seasons. For instance, some pitches RelHeight were coming in negative, this is impossible so I had to do some gameplanning on the best way to fix this. If I were to set a min and max of the average RelHeight of 6' it would completely wipeout submariners and some sidearm pitchers. What I ended up doing was taking each pitcher's respective average RelHeight and setting a window of +-1.5ft for each pitcher.

_#Stuff+_
I built the Stuff+ side of this app by first writing down targets for the machine learning model and then comparing what I had, to what was already out there. At first, I was going to use whiffs as my target. But after some research, I landed on xRV as my target value for each pitch as this is what I found to be the "entire story" of every pitch and there is too much variance that can happen with just using whiffs.

_#Tunneling_
For the tunneling metrics, I took the average path in x, y, and z for each of the pitcher's pitches. I then took the balls position at the "commit point" (180ms before the plate) and compared the distance it was to every other pitches commit point. Once you have that, you can look at the difference those pitches are when they get to the plate. For instance, if a pitchers 4Seam and Slider are 0.3" apart at the commit point and 13" apart when they reach the plate, these two pitches tunnel well together and give a high tunneling score. However, there is a penalty depending on release point difference that drops the tunneling score.

_#Limitations_
One thing that I would change and look into is Trackman's systems and the best way to get around the radar's mistakes. I used AutoPitchType in Trackman which is basically Trackman's systems "best guess" at what the pitch type is. The main reason I did this is because the TaggedPitchType only show "Fastball" and there is no distinction between 4S or 2S and that was a deal breaker for me. However, that does mean I'd have to take the hit of AutoPitchType's mistakes. For example, a sidearmer throwing a 4S can come in as a Sinker or 2S just because of the shape of the pitch. So in the future I want to find ways to get around the radar's mistakes

_#What's Next_
What I am working on now and will be in the future is a pipeline that automatically cleans and feeds each new game CSV straight to my Stuff+ & Tunneling app and any future apps that I make.
