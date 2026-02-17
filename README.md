# 🕯️ Efteling Danse Macabre WLED Lantern Mod

A hardware mod project where I upgraded the official **Danse Macabre popcorn lantern** from the Efteling into a fully programmable WLED-powered lantern with dynamic flame effects.

The original lantern already looked amazing, but the stock orange LEDs could be improved. So I rebuilt the internals to make the lantern truly *come alive* while preserving the original aesthetic.

---

## 🎥 Demo

[Click here to watch the demo on YouTube](https://youtube.com/shorts/hM2XBhFmyak?feature=share)

---

## ✨ What This Mod Does

This mod transforms the Danse Macabre popcorn lantern into something that feels a little more… alive.

The original lantern already captures the atmosphere of the dark ride beautifully, but internally it has been completely reimagined:

- The stock orange LEDs are replaced with fully addressable LEDs
- An ESP32 running WLED now controls the internal light show
- Multiple dynamic flame and ember-style presets inspired by the dark, mysterious tone of Danse Macabre
- A discreet physical button allows toggling the lantern on or off and cycling through effects
- The original AAA battery compartment is replaced with a regular powerbank
- From the outside, the lantern still looks completely original - the magic happens within
- 
---

## 🔧 Hardware and Tools Used

### Hardware

- 1x ESP32 DevKit V1 (USB-C)
- ~ 3 meters of WS2812B addressable LED strip (60 LEDs/m, ±180 LEDs total)
- 330Ω resistor (data line protection)
- 470µF capacitor or higher (power stabilization between 5V and GND)
- 1x momentary push button
- Frosted glass spray **or** a piece of white parchment paper (to create a diffused, frosted-glass look)
- 1x regular powerbank (5000+ mAh recommended)
- USB-C to USB-C cable (to power the ESP32)
- Hook-up wires in at least 3 colors (e.g. red = 5V, black = GND, white/green = data)
- 1x PVC tube, approx. 18 cm long and ±75 mm in diameter  
  *(Slightly smaller is fine, as long as the ESP32 and powerbank fit inside comfortably.)*

### Tools

- Screwdriver
- Pliers for cutting wires
- Soldering iron + solder
- Hot glue gun
- Wire stripper / cutter
- Multimeter (recommended for testing connections)

---

## ⚡ Wiring Overview

Basic wiring:

ESP32 VIN → LED 5V  
ESP32 GND → LED GND  
ESP32 GPIO → 330Ω resistor → LED DIN  
1000µF capacitor between 5V and GND  
Push button between GPIO and GND  

Make sure:
- The LED strip is connected to **DIN**, not DOUT
- Common ground is shared
- Capacitor polarity is correct

---

## 🧠 WLED Configuration

- LED type: WS2812B
- Color order: GRB
- Matrix layout configured for cylindrical spiral
- Button type: Pushbutton
- Preset cycle via macro

Preset cycle macro used:

