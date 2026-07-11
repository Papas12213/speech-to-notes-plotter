# VoiceScript 
 A pen plotter that physically writes down whatever you say to it. It's like speech-to-text, but now it's actually writing.
 
 [ video ]

 # Try it yourself
 If you have a machine that can process G-code, connect it to your computer. While I use a custom-made 3D-printed pen holder, it is not necessary. You can just zip-tie a pen onto the head like I originally did. Then, run the file [`talk_to_plot.py`](./talk_to_plot.py) on your terminal or IDE. From there, simply follow the instructions and click Enter to start. 
 *Note: Since my plotter does not have a z-axis, the code does not include Z commands, which could cause issues on certain machines (This will be updated later to accommodate all types of machines)*

 Don't have a plotter but want to see it in action for yourself? Here's me saying multiple different phrases:

 [ video ]

 # Features
 - Using [SpeechRecognition](https://pypi.org/project/SpeechRecognition/) and [Hershey Fonts](https://pypi.org/project/Hershey-Fonts/), my code converts speech into mappable G-code. This G-code is then automatically sent to a plotter, allowing spoken words to be written down on a piece of paper.

 - The pen is held up by a 3D-printed pen holder made in Fusion 360. The holder uses the pen's own weight to keep the pen stable, allowing for smooth and non-blotchy text.

 - Since my plotter does not have a z-axis, the pen will drag across the paper, causing streaks that ruin the writing. I have worked around this by providing stop points for the user to lift up the pen and prevent these long lines from happening.

 -  The user can easily change the size of the font by changing the [FONT_SIZE](https://github.com/Papas12213/speech-to-notes-plotter/blob/9c4db8eda4f29700cc667a0df30038a5cd3fbb04/talk_to_plot.py#L11), allowing for more words to be written. The only limitations are the dimensions of the machine.

 - The user also has the ability to use whatever font they want, given that it is available in Hershey Fonts. I recommend using the cursive font as it has the least amount of lifting.

 - While I wrote the code based on my current plotter using only the X and Y axes, the code should work for any machine that can take G-code (CNCs, 3D printers, laser cutters, etc.)

# Requirements 
> Note: The code was written especially for my plotter. While it will still work on other machines, the code is based on my plotter's dimensions, axes, and baud rate, so certain movements may be very short or may not even happen, especially on machines with a z-axis and nozzles/lasers. These are all decided with variables that can be changed to accommodate your machine, although I do not include z-coordinates in my code.

- The entire code is written in Python. I currently use Python 3.13, but any version of Python 3 will work. You will also need to install the following libraries: Pyserial (imported as serial), HersheyFonts, PyAudio, and SpeechRecognition.

- An internet connection. Your words are turned into digital text by [SpeechRecognition](https://pypi.org/project/SpeechRecognition/), and there are multiple different APIs available for it. I use Google's Web Speech API because of its high accuracy, but this requires an internet connection. Alternatively, you could use PocketSphinx (CMU Sphinx), which allows you to run the code offline, but it has a lower accuracy.

- A machine that can run G-code, preferably one with only an X and Y axis, but any will work. Additionally, a wired connection is preferred, but a Bluetooth connection is included and works as well.

- An attachment to hold the pen in place. While I use *this* attachment, you could also just zip-tie a pen onto the head of your machine.

- A microphone is needed for your voice to be recorded and converted into text.

# How it Works
The code is broken down into 3 steps: 
1. Voice Capture
      - When you first speak into your microphone, SpeechRecognition converts your words into a digital string of text. This is needed to convert your words into G-code.
2. Translation to G-code
      - Now that your words are a digital string of text, the speech_text_to_grbl_gcode function uses HersheyFonts to find the coordinates needed to map out every letter in your sentence. It calculates the X and Y coordinates for every line segment, and these coordinates are then input into the G-code format. This is the part that makes your words mappable.
3. Execution 
      - The G-code is now sent to your plotter/machine. Since my plotter's dimensions are limited, it monitors the current x/y coordinates and compares them against the plotter's max dimensions. When the plotter finishes a word and notices it cannot fit the next word in the given space, it will pause and tell the user to lift the pen so that it can create a new line to continue the sentence.

Since my plotter doesn't have a z-axis (it's an old laser cutter I found on the side of the road), I had to make a few workarounds. Since the pen would normally drag when moving onto a new line or when homing, I added stop points where the user must lift the pen before the machine can continue. This prevents those huge line streaks that would normally happen. Knowing this, I also updated my pen holder so that the pen could easily be removed. My first version needed the user to constantly screw and unscrew a screw, so I changed it so that the pen's weight keeps it stable.

# Pen Holder
 Unnoficial version:
   - Zip tie. My plotter has 2 holes on the head, so I wrapped a zip tie around these holes, stuck a pen inside, and tightened it as hard as I could. While it works, the pen was kind of hard to remove and would sometimes come lose.

Version 1:
   - First actual version, designed in Fusion 360 and then 3D printed. It features 3 holes for screws and a large holding area that can fit multiple different pens. The top 2 holes are for screws and are meant to mount the holder onto my plotter. The side screw it used to tighten the holding area and prevent the pen fron moving.


| Pros | Cons |
| --- | --- |
| Can hold many different pen sizes | he side screw either forces the pen to be too high or too low, making the writing barely visible or super blotchy |
| Can easily keep pens stable and in place | When the plotter moves onto a new line, it's very impractical to untighten and tighten the side screw over and over |

