# 🕯️ Efteling Danse Macabre WLED Lantern Mod

A hardware mod project where I upgraded the official **Danse Macabre popcorn lantern** from the Efteling into a fully programmable WLED-powered lantern with dynamic flame effects.

The original lantern already looks amazing, but the stock orange LEDs could be improved. So I rebuilt the internals to make the lantern truly *come alive* while preserving the original aesthetic.

---

## 🎥 Demo

[Click here to watch the demo on YouTube](https://youtube.com/shorts/hM2XBhFmyak?feature=share)

![Result](https://github.com/LethalRabbit/efteling-danse-macabre-wled-lantern/blob/d6b8cb45dc4eade148d3c2785d11ecf73ecba6bf/images/Result.jpg)

---

## ✨ What This Mod Does

This mod transforms the Danse Macabre popcorn lantern into something that feels a little more... alive.

The original lantern already captures the atmosphere of the dark ride beautifully, but internally it has been completely reimagined:

- The stock orange LEDs are replaced with fully addressable LEDs
- An ESP32 running WLED now controls the internal light show
- Multiple dynamic flame and ember-style presets inspired by the dark, mysterious tone of Danse Macabre
- A discreet physical button allows toggling the lantern on or off and cycling through effects
- The original AAA battery compartment is replaced with a regular powerbank
- From the outside, the lantern still looks completely original - the magic happens within

---

## 🟢 Difficulty Level: Easy

This project is designed to be beginner-friendly.

You do **not** need programming knowledge.  
You do **not** need advanced electronics experience.

However, you should:

- Be comfortable with **basic soldering**. If you have never soldered LED strips before, do yourself a favour and look up a short YouTube tutorial. You will save yourself a lot of time and frustration by mastering the basics first.
- Be able to follow instructions carefully
- Take your time and double-check connections

If you can solder a few wires and follow step-by-step instructions, you can build this lantern.

This guide is written for non-technical makers - including cosplayers, prop builders, and hobbyists - and explains each step as clearly as possible so anyone can recreate the project. Just follow the steps in order and don’t rush the wiring. 

If you are a technical person who is comfortable with soldering and wiring circuit boards, you can probably skip some portions of this guide.
  
---

## 🔧 Hardware and Tools Used

### Hardware

- 1x ESP32 DevKit V1 (USB-C)
- ~ 3 meters of 5V WS2812B addressable LED strip (60 LEDs/m, ±180 LEDs total)
- 330Ω resistor (for data line protection)
- 470µF capacitor or higher (power stabilization between 5V and GND)
- 1x momentary push button
- Frosted glass spray **or** a piece of white parchment paper (to create a diffused, frosted-glass look)
- 1x regular powerbank (5000+ mAh recommended)
- USB-C to USB-C cable (to power the ESP32)
- Hook-up wires in at least 3 colors (e.g. red = 5V, black = GND, white/green = data)
- 1x PVC tube, approx. 18 cm long and ±75 mm in diameter  
  *(Slightly smaller is fine, as long as the ESP32 and powerbank fit inside comfortably. A larger diameter is not advised, as the LEDs may end up too close to the glass and be individually visible from the outside)*

### Tools

- Screwdriver
- Pliers for cutting wires
- Soldering iron + solder
- Hot glue gun
- Glue stick
- Wire stripper / cutter
- Scissors
- Hobby knife
- Multimeter (recommended for testing connections)

---

# 🛠 Build Guide

This section explains how to create the lantern step by step.

No advanced coding is required. We will use existing firmware (WLED) and configure it.

---

## 1️⃣ Install WLED on the ESP32

Before wiring anything, we first install WLED on the ESP32 board.

WLED is open-source firmware for controlling addressable LEDs:  
https://github.com/wled/WLED

The easiest way to install it is via the official web installer:  
https://install.wled.me/

### Step-by-step installation

1. Plug your ESP32 board into your computer using a USB-C cable.
2. Open **Google Chrome or Microsoft Edge** (recommended for best compatibility).
3. Go to:  
   👉 https://install.wled.me/
4. Click **Install**
5. Select your ESP32 device from the list that appears.
6. Confirm the installation.
7. Wait until the process finishes.

When the installation completes, you may see an option to continue with WiFi configuration (connecting to your home network, etc.).

For this project, we will **not** connect the ESP32 to your home WiFi.  
Instead, we will let it create its own WiFi network. This allows you to adjust the lantern settings anywhere - even inside the Efteling or on a convention - without needing internet access.

So skip the additional configuration steps for now.

### Connect to the WLED Access Point (WLED-AP)

After installing WLED, the ESP32 should automatically start broadcasting its own WiFi network.

1. On your laptop or smartphone, open your WiFi settings.
2. Connect to the network called:  
   **WLED-AP**
3. The default password is:  
   **wled1234**

Once connected:

4. Open a browser and go to:  
   http://4.3.2.1  
   or  
   http://wled.me  

If the WLED interface loads, the installation was successful 🎉.

### (Optional) Rename the WiFi Network

It is **strongly** advised to change the default WiFi Network name and password, so that not everyone with WLED knowledge can mess with your lantern's configuration.

1. Open WLED.
2. Go to **WIFI SETTINGS**
3. Scroll down to AP SSID and change the name and password.
4. Click **Save**
5. Restart the board.

Reconnect to the new WiFi network using your updated password.

We will now continue to the wiring steps. Put your ESP32 board aside for now, we will need it again later.

---

## 2️⃣ Soldering the LED strip and wrap around PVC tube

Before connecting anything to the ESP32, we first prepare the LED strip.

### Step 1 - Prepare the Wires

- Cut three pieces of wire (red, black and white), approximately **10 cm (4 inches)** long.
- Strip both ends of each wire.
- Tin the exposed wire ends with a small amount of solder.

### Step 2 - Identify the Correct End of the LED Strip

⚠️ This step is very important. WS2812B LED strips have a direction. Look closely for the small arrows printed on the strip. You must solder your wires to the pads labeled:

**5V – DIN - GND**

Do **not** solder to the side labeled:

**5V – DOUT - GND**

The arrow should point *away* from the ESP32. If you accidentally connect to DOUT instead of DIN, the LEDs will not respond.

### Step 3 - Solder the Wires

Using the following color convention (recommended):

- 🔴 Red → 5V  
- ⚫ Black → GND  
- ⚪ White → DIN (Data In)

### Step 4 - Prepare the PVC Tube

- Take your PVC tube.
- Cut a small hole near the bottom edge on one side.
- This hole allows the three wires to pass through to the inside.

### Step 5 - Wrap the LED Strip

- Start at the bottom of the tube.
- Wrap the LED strip in a spiral pattern all the way to the top.
- Keep spacing consistent for the best flame effect.
- Secure the strip using hot glue if necessary. You can also apply some hot glue to the soldering connections for extra protection.

After wrapping the LED strip around the tube, your result should look similar to the image below.

![LEDs wrapped](https://github.com/LethalRabbit/efteling-danse-macabre-wled-lantern/blob/d6b8cb45dc4eade148d3c2785d11ecf73ecba6bf/images/LEDs%20Wrapped.jpg)

It's possible to create an extra barrier between the bottom (where the electronics will live) and the top (where we will place the powerbank) of the PVC tube. In order to do so, I added a lid inside and cut a hole in it to feed the USB-C cable through.

![Separation lid](https://github.com/LethalRabbit/efteling-danse-macabre-wled-lantern/blob/82e3b34d2d202679b84af3cb49afca1adbe456e9/images/Cable%20Hole.jpg)

That concludes the first step. On to soldering the LED strip to the ESP32 module!

---

## 3️⃣ Soldering the Capacitor and Resistor

Now that the LED strip is wrapped around the PVC tube and the three wires are attached, we will add the resistor and capacitor to our setup.

### Step 1 - Soldering the Resistor to the Data Line

For extra protection against high currents, the data line (white) must go through a 330Ω resistor before reaching the ESP32.

1. Take your 330Ω resistor.
2. Cut the legs shorter if needed.
3. Slide a small piece of heat shrink tubing onto the white data wire **before soldering** (important - you can’t add it later).
4. Solder one leg of the resistor to the white wire coming from the LED strip.
5. Slide the heat shrink tubing over the exposed solder joint.
6. Use a heat gun or lighter carefully to shrink it.

You should now have: White wire → 330Ω resistor → free resistor leg. 

We will add an additional piece of white wire to the free resistor leg, in order to make isolating it with shrink tube easier:

1. Cut a short extra piece of white wire (about 5–8 cm)
2. Solder it to the remaining free resistor leg.

### Step 2 - Combine 5V and GND with Capacitor (Parallel Connection)

The capacitor must be connected **in parallel** between 5V and GND. Instead of soldering everything directly onto the ESP32 pin, we first create a clean junction.

#### For the 5V side:

1. Cut a short extra piece of red wire (about 5–8 cm).
2. Slide a piece of heat shrink tubing onto the red LED wire.
3. Twist together:
   - The red wire from the LED strip
   - The long leg of the capacitor (⚠️ Important: this **must** be the long leg / positive side)
   - One end of the extra red wire
4. Solder these three together.
5. Slide the heat shrink tubing over the joint.
6. Shrink it.

You now have: (LED 5V + capacitor positive) → extra red wire → free end

#### For the GND side:

1. Cut a short extra piece of black wire (about 5–8 cm).
2. Slide heat shrink tubing onto the black LED wire.
3. Twist together:
   - The black wire from the LED strip
   - The short leg of the capacitor (⚠️ Important: this **must** be the short leg / negative side)
   - One end of the extra black wire
4. Solder these three together.
5. Slide the heat shrink tubing over the joint.
6. Shrink it.

You now have: (LED GND + capacitor negative) → extra black wire → free end

⚠️ Make absolutely sure the capacitor legs can not touch each other, and are fully wrapped in shrink tubing.

---

## 4️⃣ Soldering the LED strip to the ESP32 board

After completing the previous step, you should now have ended up (again) with a red, black and white wire.

Now, we will connect the wires to the board. 
⚠️ A couple of notes:
- Before soldering each wire, make sure to add some shrink tube to the wire first.
- Add some flux and solder to the ends of the wires, as well as to the following ESP32 pins:
  - VIN
  - GND
  - D25

We will solder the wires to the following pins:
- Red wire → ESP32 VIN
- Black wire → ESP32 GND
- White wire → ESP32 D25

Solder each one carefully. After soldering, slide the shrink tube over it and shrink it. You should end up with a result that looks like this:

![Wiring Result](https://github.com/LethalRabbit/efteling-danse-macabre-wled-lantern/blob/82e3b34d2d202679b84af3cb49afca1adbe456e9/images/LED%20Wiring.jpg)

---

### Final Check Before Powering

Before plugging in USB power:

- Verify red goes to VIN.
- Verify black goes to GND.
- Verify capacitor polarity is correct.
- Verify white wire goes through the resistor to the GPIO.
- Make sure there are no loose strands of wire.

Now:

1. Plug the ESP32 into USB power.
2. Open the WLED interface.
3. Turn the LEDs on.

If everything is wired correctly, the LED strip should light up.

If nothing happens, first check:
- Did you connect to DIN and not DOUT?
Then create a preset with the following API command:

