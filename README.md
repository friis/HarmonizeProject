Harmonize Project for Philips Hue 
============================
Harmonize is a low latency video analysis and pass-through application built in Python which alters Philips Hue lights based on their location relative to a screen; creating an ambient lighting effect and expanding content past the boundries of a screen. [Watch the demo here!](https://www.youtube.com/watch?v=OkyUntgiYzQ)

Currently in development - Expected release in August 2020

Due to litigation with Signify (Owner of the Philips Hue brand), our website was taken down. Harmonize Project (formerly known as Harmonize Hue) - This project has no affiliation with Signify or Philips Hue.

# Features:
* Low Latency loop-through HDMI output
* Location based light changes
* Streaming to Hue Lights via Entertainment API
* Sending 50-75 color updates per second

# Requirements 
Hardware: (Tested on Raspberry Pi 4B)
* RAM: 512MB Minimum (No swap needed)
* CPU: 1GHz minimum, 4 Cores strongly reccomended (Application runs 3 threads and leaves 1 core to handle other tasks.)
* HDMI Splitter (Must be able to output 4k & 1080/720p simultaneously) [Here is a good one.](https://www.amazon.com/gp/product/B07YTWV8PR/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)
* USB3.0 HDMI Capture Card (Capable of capturing 720/1080p) [I got this one for $45.](https://www.amazon.com/gp/product/B07Z7RNDBZ/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) A similar one should be fine.

Software:
* Python3 (Project written and tested on 3.6)
* pip3
* Screen (if you intend to run this on a headless server)
* v4l2 (You may need a different driver based on your HDMI->USB Capture card. Information on drivers for cheap video cards is [here](https://linuxtv.org/wiki/index.php/Easycap#Making_it_work_4))

Python Modules:
* sys
* http_parser
* argparse
* requests
* time
* json
* pathlib
* socket
* subprocess
* threading
* fileinput
* numpy
* cv2 (Also known as OpenCV. You may have to compile from source depending on your setup. Guides are a Google search away.
* mbedtls (python-mbedtls, may also have to be compiled from source.)

# Installation

git clone https://github.com/MCPCapital/harmonizeproject.git

cd harmonizeproject

# Usage

./harmonizeproject.py -c -a -s 

-v (verbose)

-g {#} Use specific entertainment group number

Configurage things
* 'breadth' within function 'averageimage' - determines the % of the edges of the screen to use in calculations. Default is 15%.
* 'if ct % 1 == 0:' within funciton 'cv2input_to_buffer' - Edit to skip frames if performance is poor on your device. 
* 'time.sleep(0.005)' within funciton 'buffer_to_light' - Determines how frequently messages are sent to the bridge. Keep in mind the rest of the function takes some time to run in addition to this sleep command. Bridge requests are capped by Philips at about 100 if I recall correctly.
