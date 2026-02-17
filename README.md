# 🕯️ Efteling Danse Macabre WLED Lantern Mod

A hardware mod project where I upgraded the official **Danse Macabre popcorn lantern** from the Efteling into a fully programmable WLED-powered lantern with dynamic flame effects.

The original lantern already looked amazing, but the stock orange LEDs could be improved. So I rebuilt the internals to make the lantern truly *come alive* while preserving the original aesthetic.

---

## 🎥 Demo

[Click here to watch the demo on YouTube](https://youtube.com/shorts/hM2XBhFmyak?feature=share)

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

- Be comfortable with **basic soldering**
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

---

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

---

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

---

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

## 2️⃣ Wire the ESP32 and LED Strip

Now that WLED is installed, we can start wiring.

### LED Strip Preparation

Before connecting anything to the ESP32, we first prepare the LED strip. If you have never soldered LED strips before, do yourself a favour and look up a short YouTube tutorial. You will save yourself a lot of time and frustration by mastering the basics first.

- Cut three pieces of red, black and white wire, approximately **10 cm (4 inches)** long.
- Strip the ends of the wire and solder them to the LED strip.

In this guide, I used the following color convention:

- 🔴 Red → 5V  
- ⚫ Black → GND  
- ⚪ White → DIN (Data In)

Using different colors is highly recommended to avoid confusion later.

### Connections

ESP32 VIN → LED 5V  
ESP32 GND → LED GND  
ESP32 GPIO (e.g. GPIO 4 or 16) → 330Ω resistor → LED DIN  
470µF capacitor between 5V and GND  
Push button between chosen GPIO and GND  

⚠ Important:

- Make sure you connect to **DIN**, not DOUT (check the arrow on the LED strip).
- The arrow should point *away* from the ESP32.
- The capacitor has polarity:
  - Long leg → 5V
  - Short leg (striped side) → GND
- All GND connections must be shared.

Before continuing:
- Power the ESP32 via USB
- Test if the LEDs light up in WLED

If they do, wiring is correct.

---

## 3️⃣ Physical Assembly Inside the Lantern

Once everything works electronically, you can mount it inside the lantern.

### LED Mounting

- Wrap the LED strip around the PVC tube in a spiral.
- Keep spacing consistent for best flame effect.
- Secure the strip using hot glue.

### Diffusion

To achieve a smooth flame look:

- Use frosted glass spray on the inner container  
OR  
- Wrap white parchment paper around the tube

Good diffusion is more important than higher LED density.

### Electronics Placement

- Place the ESP32 and powerbank inside the PVC tube.
- Route the USB-C cable through a small hole in the base.
- Replace the original AAA battery compartment with the powerbank.
- Secure components with hot glue to prevent movement.

Make sure nothing can short or touch exposed metal contacts.

---

## 4️⃣ Configure WLED

Now we configure WLED for the lantern.

Open the WLED web interface.

### LED Preferences

Go to:

Config → LED Preferences

Set:

- LED Type: WS2812B
- Color Order: GRB
- Total LED Count: (enter your actual number, e.g. 180)
- GPIO: the pin you used (e.g. 4 or 16)

Save and reboot.

---

### Button Setup

Still in LED Preferences:

- Button type: Pushbutton
- Button GPIO: the pin you connected the button to

Save and reboot.

---

### Preset Cycling

Create your flame presets.

Then create a preset with the following API command:

