# VoiceScript 
 A pen plotter that physically writes down whatever you say to it. It's like speech to text, but now its actually writing.
 
 [ video ]

 Wanna see it for yourself? Here's me saying different phrases:

 # Features
 - Using [SpeechRecognition](https://pypi.org/project/SpeechRecognition/) and [Hershey Fonts](https://pypi.org/project/Hershey-Fonts/), my code converts speech into mappable G-code. This G-code is then automatically sent to a plotter, allowing spoken words to be written down on a piece of paper.
 - The pen is held up by a 3D-printed pen holder made in Fusion 360. The holder uses the pens own weight to keep the pen stable, allowing for smooth and non-blotchy text.
 - Since my plotter does not have a z-axis, the pen will drag across the paper, causing streaks that ruin the writing. I have worked aroumd this by providing stop points for the user to lift up the pen and prevent these long lines from happening.
 -  The user can easily change the size of the font, allowing for more words to be written. The only limitation is the dimensions of the machine
 - The user has the ability to use whatever font they want (given that it is available in Hershey Fonts). I recommend using cursive as it has the least amount of lifting.
 - While I wrote the code based on my current plotter using only the x and y axis, the code works for any machine that can take G-code (CNCs, 3D printers, laser cutters, etc)
