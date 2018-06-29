# Multiplexed Library Preparation  
adapted from [Parchman et al. (2012)](http://onlinelibrary.wiley.com/doi/10.1111/j.1365-294X.2012.05513.x/full)

all microcentrifuge vials can hold 1500μL volume
___
## Digestion:
-  Start by preparing the master mix (MM1). If you are preparing 2 plates mutliply the reagents by two.
-  Take out the reagents from -20 freezer and let them thaw. Once thawed place on ice. Don't take out the enzymes (Ecor1 and MseI).
-  Vortex and centrifuge all reagents, only centrifuge the enzymes. 

**_Making Master Mix I (MMI) for Digestion (150% of what you will need)_**  
This is good for one 96-well plate. Once made, store in -20°C freezer. Always label with made-on date, MMI will expire in time (use within 3 months).  
* Label a 1.5mL microcentrifuge tube with **MMI** and into it pipette:
  * 36 μL ultrapure H<sub>2</sub>O  
  * 86.4μL 1mg/mL BSA  ... in freezer, must first dilute the stock of 20mg/mL to 1mg/mL using ultrapure H2O
  * 86.4μL 1M NaCl  ...on shelf above wet-lab prep area
  * 165.6μL 10X T4 Buffer  ... in the freezer
  * 17.28μL MseI  (10000 u/ml) ... keep in the freezer until ready to add
  * 40.32μL EcoRI  (20000 u/ml) ... keep in the freezer until ready to add

**_Digestion Protocol:_**  

1. Once the MM1 has been prepapred,vortex and centrifuge Master Mix I vials in microcentrifuge for 5s.
1. For each sample, place 6μL of genomic DNA into the assigned well of a 96-well plate
1. Add 3μL of Master Mix I to each well
1. Cover plate with sticker (i.e. microseal), seal by running finger along each row and along each column to seal wells on every side
   1. Label sticker with fat-tipped marker “**Digested [Sample X] [date] [initials]**”
   1. Label the plate itself in a similar manner
   1. Do not label with ‘Digestion’, label with ‘digested’ to emphasize past tense.
1. Vortex plate for 5s. 
1. Centrifuge at 1000xG for 20s to pull all liquid to the bottom of the wells
1. Place in Thermocycler and start the Digest Cycle (8 hours run time)
   1. ![Thermocycler program](http://4.bp.blogspot.com/-e6SPURb-Vlo/VLfyVhJRUdI/AAAAAAAAAq0/CZXib9eSYtM/s1600/unnamed.jpg) 
1. Once cycle has completed, place in 4°C refridgerator in the section labeled "**Ready for Ligation**".

___


## Ligation:
**_Making Master Mix II (MMII) for Ligation (125% of what you will need)_**  
This is good for one 96-well plate. Once made, store in -20°C refridgerator.  Always label with made-on date, MMII will expire in time. 
_Note that the official protocol calls for addition of MseI adaptor to Master Mix II, we DO NOT add it to this Master Mix since it is included in the ligation protocol below_  
* Label a 1.5mL microcentrifuge with "**MMII**"  
* Take out the reagents from -20 freezer and let them thaw. Once thawed place on ice using the black bucket and ice in autoclave/equipment room. Don't take out the enzymes (T4 DNA ligase).
* Vortex and centrifuge all reagents for a few seconds. Only centrifuge the enzymes. 
* Into MM2 pipette:
  * 8.64μL ultrapure H<sub>2</sub>O
  * 12μL 10X T4 DNA Ligase Buffer  
  * 6μL 1M NaCl  
  * 6μL 1mg/mL BSA (not the concentrated BSA)  
  * 20.1μL T4 DNA Ligase  

**_Ligation Protocol_**  

1. Before you start make sure there is enough annealed Ecor1 and MseI annealed adaptors. If not, follow the method available on GitHub-EckertLab protocols.
1. Let the annealed adaptors thaw. Once thawed either place them in the fridge or on ice.
1. Once thawed, spin digested product in centrifuge at 1000xG for 20s.
1. Spin Master Mix II vials (labeled as MMII or MM2) in the microcentrifuge for 5s.
1. Add 0.6μL of Master Mix II to each well
1. Spin the thawed annealed EcoRI and MseI plates at 1000xG for 20s.
1. Orient EcoRI and MseI plates in steps 6-7 to match ligation plate orientation
1. Did you orient the plates from Step 5??
1. Are you sure you oriented the plates correctly??
1. Using the multichannel pipette, add 1μL of annealed EcoRI adaptor to each well (this should be a plate)
   1. Always check to make sure each tip has liquid, some wells may be empty
   1. If empty you CANNOT PULL FROM OTHER WELLS!
   1. Once complete, replace tin sticker and label with fat-tipped marker. Note on label if there are any empty wells.
   1. Check to make sure writing on plate (not sticker) is not fading. If so, rewrite using fine-tipped marker on another part of plate. Don’t write over!
1. Using the multichannel pipette, add 1μL of annealed MseI adaptor to each well (this should be a plate)
   1. Always check to make sure each tip has liquid, some wells may be empty.
   1. If empty, you can pull from other wells YOU CANNOT DO THIS WITH ECORI
   1. Once complete, replace tin sticker and label with fat-tipped marker. Note on label if there are any empty wells.
   1. Check to make sure writing on plate (not sticker) is not fading. If so, rewrite using fine-tipped marker on another part of plate. Don’t write over!
1. Cover ligation plate with sticker, seal by running finger along each row and along each column to seal wells on every side
   1. Label with fat-tipped marker “*Ligated [Sample X] [date] [initials]*”
   1. Label the plate itself in a similar manner  
   1. Do not label with ‘ligation’, label with ‘ligated’ to emphasize past tense.  
1. Vortex plate for 5s.  
1. Centrifuge ligation plate at 1000xG for 20s to pull all liquid to the bottom of the wells
1. Place in Thermocycler and start the Ligation cycle (6 hours run time)
   1. ![Thermocycler setting](http://2.bp.blogspot.com/-ytBH1GGjlDM/VLfyV20iqaI/AAAAAAAAAqw/io6rOJAdFKo/s1600/unnamed-1.jpg)
1. Once cycle has completed, place in 4°C refrigerator in section labeled "**Ready for PCR**"
1. As soon as ligation is done add 189μl of 0.1X TE buffer (NOT TAE) to each well to dilute the products and also avoid samples being evaporated. 
1. If you think you will not be using these products for a while place them in -20*C.


___

## PCR
**_Making 380μL of 5μM PCR primers for Master Mix III_**  
This is enough for all three vials of MM3 needed. Once made, store in -20°C freezer.  Always label with made-on date, MMIII will expire in time. 
  * Label a 1.5mL microcentrifuge tube with "**PCR Primers**"
  * Vortex and centrifuge the thawed Primers (F and R) before preparing the PCR Primers.
  * Into it pipette:  
    * 10μL 100μM Illpcr F Primer  
    * 10μL 100μM Illpcr R Primer  
    * 360μL ultrapure H<sub>2</sub>O  

**_Making 100μL of 10mM dNTP mix for Master Mix III_**  
This is enough for all three vials of MM3 needed. Once made, store in -20°C freezer. Always label with made-on date, dNTPs will expire in time. 
  * Label a 1.5mL microcentrifuge tube with "**dNTP Mix**"  
  * Vortex and centrifuge the thawed dNTPs before preparing the dNTP mix.
  * Into it pipette:  
    * 2.5μL of each 100mM dNTP (A, C, T, G)  
    * 90μL ultrapure H<sub>2</sub>O

**_Making Master Mix III for PCR (125% if what you will need)_**  
  * You will need to make 3 vials of this Master Mix for the two 96 well plates. Once made, store in -20°C refridgerator. Always label with made-on date, dNTPs and polymerase will expire in time.
  * Vortex and centrifuge the thawed reagents before adding them the MM3 vials. Don't vortex or thaw the polymerase.
  * Once thawed place all reagents on ice except DMSO.
  * When vial is empty, spin down before throwing away, use any remaining. Polymerase is expensive! 
  * Label 3 microcentrifuge vials with MM3 on lid AND side of vial. Into each place:
    * 773.6μL ultrapure H2O (770μL + 3.6μL)  
    * 320μL 5X Iproof HF Buffer (green vial)  
    * 32μL 10 mM dNTP Mix  
    * 32μL 50mM MgCl2  
    * 106.4μL 5μM PCR Primers  
    * 12μL DMSO (6μL + 6μL)  
    * 16μL Iproof Taq Polymerase (DO NOT ADD UNTIL READY TO PLATE!)  
  * Vortex then spin down the vials of MM3 using the microcentrifuge for 5-10s.
  

**_PCR Protocol_**  

1. If opening a new box of ingredients, label with date and your initials with fine-tipped permanent marker
1. Centrifuge ligated-diluated samples at 1000xG for 20s to pull down liquid.
1. If your ligated products are not diluted with 1xTE you can add it now.
1. Get two new 96-well plates and label ON THE PLATE with fine-tipped permanent marker “**PCR Product [sample] [date] [initials]**”
1. Orient these plates in the same direction as ligated plate!
   1. Using the multichannel pipette, add 4μl of the diluted, ligated, samples to the 2 NEW plates – DO NOT REUSE PIPETTE TIPS except for the same row across the two plates
1. Add 16μl of Master Mix III to each well
1. Place tin sticker on new plates and label with fat-tipped marker “**PCR Product [sample] [date] [initials]**”
   1. Do not label with just ‘PCR’, label with ‘PCR Product’ to emphasize past tense.
1. Centrifuge at 1000xG for 20s to pull all liquid to the bottom of the wells
1. Place plates in Thermocyclers and start the PCR cycles (55.5 minutes run time)
   1. ![Thermocycler setting](http://4.bp.blogspot.com/-xsMSgVGlnkE/VLfyfdTraQI/AAAAAAAAArA/1_NRwjjYqDg/s1600/unnamed-2.jpg)
1. Once cycles complete, pool samples into a sterile 15mL blue-capped centrifuge tube.
   1. Place in 4°C refrigerator in section labeled “**Ready for gel extraction**”
1. Perform [Gel Extraction Protocol](https://github.com/EckertLab/protocols/blob/master/gel_extraction_protocol.md) following completion of PCR




