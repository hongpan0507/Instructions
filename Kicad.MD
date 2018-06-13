# Schematic
## component pin electrical type
1. Input is a unidirectional input, like an input to a 7400 NAND gate.  
2. Output is a unidirectional output that can drive high or low, like the output of a NAND gate.  
3. Bidirectional can act as an input or an output. The I/O pins on microcontrollers are bidirectional.  
Tri-state is an output that can drive high or low, but can also be placed in a high-impedance state where it floats. The 74125 is a chip with tri-state outputs (sometimes called three-state outputs: hi, low, and high-impedance).  
4. Passive is an unpowered connection, like you would find on resistors, capacitors and inductors.  
5. Unspecified is, well, unspecified. I guess you would use that when no other classification fits.  
6. Power input is an pin where power comes in to a chip. Both the VCC and GND pins of chips would be classified as power inputs.  
7. Power outputs are where power comes out of a chip. The outputs of voltage regulators are the most common example of this pin type.  
8. Open collector output pins are outputs that can be driven low, but float otherwise. These are good for wired-AND connections where the output goes low if any of the attached open-collector pins goes low, but the output is pulled high by a pull-up resistor if all the pins are floating. The 7401 is a NAND gate chip with open-collector outputs.  
9. Open emitter output pins can be driven high, but float otherwise. These are good for wired-OR connections where the output goes high if any of the attached open-emitter pins goes high, but the output is pulled low by a pull-down resistor if all the pins are floating.  
10. Not-connected pins are pins which have no function. Think of these as package pins that aren't bonded to the IC inside.  

# Layout
## Automatic components placement/move
  1. Select "Mode footprint" button on the top tool bar
  2. Right click on the footprint and select "Global Spread and place" -> "Spread out all footprints" or
  3. Right click on the footprint and select "Global Spread and place" -> "automatically place all footprints" or
  4. Right click on the footprint and select "Automatically place footprint"
  
## Make any shape of footprint on any layer
  1. Use an image editor (Inkscape etc.)to draw the shape; if shape is in black, white background is required; or vice versa
  2. Save the image as bitmap file format (BMP or PNG)
  3. Open "Bitmap2Componet" from Kicad control Pane
  4. "Load Bitmap"
  5. Click on "Black&White Picture" tab
  6. Change the Threshold Value if the shape does not appear
  7. In "Options", "Normal" = no change to the orignal shape, "Negative" = invert the colors (Black to white, White to black)
  8. The "black shape" = keep-out, the "white shape" = the shape shows up in kicad footprint editor
  9. Select "Format" as "Pcbnew(.kicad_modfile)"
  10. Click on "Export", save the library file to a ".pretty" folder (footprint library folder)
  11. Load the component to double check the size, shape and resolution
  12. To change the shape to any layer, load exported file to a text editor, change "layer" to any desired layer  
    
  Note: in "Bitmap2component"
    1. Do not change Resolution; it scales the image if changed
    2. if higher resolution is needed, increase the number of pixels while maintain the physical dimension of the shape in the image editor
    3. Only "From silk screen" and "From solder mask" are available from "Bitmap2Component", but the shape can be put onto any layer by manually edit the exported file with text editor
  
## Add multiple copper fill zones
  1. create 1st zone outline
  2. set the priority to the lowest (= 0)
  3. zone priority determines which zone is to be filled up first 
  4. higher priority number gives higher priority
  5. priority must be different when create for the first time between different zones
  
## Keep-out zone for Solder Mask Layer
  Option A: Use Solder Mask Layer as Keep-out layer in Footprinter Editor
    1. In Footprint Editor, select Solder Mask Layer
    2. Make the desired pattern
    3. The pattern is the keep-out zone.
  Option B: Use fill zone as keep-out zone in Pcbnew (PCB routing)
    1. Select Solder Mask Layer
    2. Select "Add filled zone"
    3. Click on the starting point of the keep-out zone
    4. Fill out "Non Copper Zones Properties"
    5. This method works for all non-copper layer

## Change global or default thermal relief setting for pads
  1. In "Pad Properties"->"Local Clearance and setting"->"Copper Zones", Choose "Thermal Relief" for "Pad connection".
  2. Set Values for "Thermal Relife width" and "Thermal Relife gap"; if "0" is used, it will use the global value instead
  3. To change the global value,"Edit copper zone properties"->"Pad Connection", choose "Thermal Relief"; 
     "Antipad clearance" = "Thermal Relife gap"
     "Spoke width" = "Thermal Relife width"
  4. Change "Pad connection" back to "solid" if only specific pads are required to have thermal relief

## Pad clearance setting
  1. Right click on the footprint -> "Edit Footprint Parameters" -> "Pad Clearance"; It only sets the clearance locally.
  2. Setting pad clearance globally, Not found yet
        
## Add footprint library 
  1. In PCB layout or footprint editor: Preferences->Footprint Library Manager->append with wizard->KiCad
    ->Use path relative to the project->Add FP Libraries->select all the folders (.pretty) that contatins the footprint
  2. Instruction to set environmental path and more: https://lists.launchpad.net/kicad-developers/msg12945.html

# 3D output
## 3D module
  1. Kicad variable environment sets the location where the 3d module is saved.
  2. The default kicad variable environment is most likely not going to work.
  3. To create or change in Windows, "System Properties" -> "Advanced" -> "Environment Variables" -> "System Vairables",
     create a new one if the variable name "KISYS3DMOD" and "KISYSMOD" do not exist, the value of the variable is the path
     which points to the folder where 3D module is saved.
  4. Restart of the PC maybe required.
  5. More info and Linux setting: https://lists.launchpad.net/kicad-developers/msg12945.html
  6. Many 3D models can be downloaded from the web.
      Examples: http://www.3dcontentcentral.com/Default.aspx
                https://grabcad.com
                Manufacture Website
  
## Build and add 3D module for a footprint
  1. Create or download 3d module (stl, step files)
  2. Open up using solidworks; adjust color, dimension, and rotation if necessary
  3. save as .wrl file; click on the "option", and make sure the unit is in "mm"; (KiCad accepts wrl 2.0 file)
  4. In the kicad footprint editor, click on footprint property, 3d shape setting, add the 3d shape in wrl format
  5. set the scaling to 1/2.54; (1inch/2.54cm)

# Others
## turn off "invisible text"
  1. In Pcbnew (layout), Click on "Render" on the right hand size, next to "layer" tab, uncheck "hidden text"
  2. All the layer, footprint, via etc can be set invisible
  
## plugin location
  1. "C:\Program Files\KiCad\share\kicad\scripting\plugins"
