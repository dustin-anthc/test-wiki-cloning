# AKWarm Energy Tax Credit Protocol

-  [[Overview|#tax-protocol-overview]]
-  [[Protocol|#protocol]]
-  [[Specifications for the Standard Reference and Proposed Designs|#reference-specs]]
-  [List of Cities and Weather Factors](https://docs.google.com/spreadsheets/d/1tOSD73M5SEScmzKY7QV3m2U646YDWh9yAGOrIRRzUHo/edit?usp=sharing)
-  [[Tax Credit FAQ|#tax-credit-faq]]


----------

<a name="tax-protocol-overview"></a>
### Overview

In July 2005 Congress passed the 2005 Energy Policy Act. The legislation provided for a tax credit to builders for building energy efficient homes. To meet the energy saving requirements, a home must use no more than 50% of the energy used by a home built to 2004 International Energy Conservation Code (IECC) standards. The only way to determine if a home will qualify for the tax credit is to have an analysis done using one of the software programs approved by the IRS. AKWarm has been approved as a software program for this purpose *when used in compliance with this ENERGY TAX CREDIT PROTOCOL.*

In order to use AKWarm to show that the proposed home uses no more than 50% of the energy used by a home built to 2004 IECC standards, the Energy Rater must make 2 different AkWarm files, one incorporating the energy components as defined by the 2004 IECC standards, and the second file incorporating actual components to be used in the home. BOTH FILES MUST BE SUBMITTED TO AHFC FOR REVIEW AND WILL BE RETAINED BY AHFC.

<a name="protocol"></a>
### Protocol

1.  REFERENCE HOME: Create an IECC Standard Reference Home, using the component values from IECC 2004, as described in Table 1, below. Save this file with a unique name, beginning with the letter R-.

2.  PROPOSED HOME : Using this same file, rename it to start with the letter P-, and change the building components to those in the actual Proposed Design.

3.  ENERGY USE CALCULATION: Using the AkWarm outputs for space heating only, calculate the total annual energy use (BTU/yr) for each case as follows

	**Q (BTU/yr) = [E + V] x 3,413 (BTU/kWh) + F x C**

	 *where:*

     	E = the annual amount of electricity used for space heating (kWh/yr)
     	V = the annual amount of vent fan energy from mechanical ventilation specification below (kWh/yr)
     	{NB: for proposed case, V is always zero}
    	F = the annual amount of fuel used for space heating in the AkWarm output units (gallons, ccf, etc)
     	C = the conversion from the fuel units to BTU, for example,
     	C (fuel oil) = 138,000 BTU/gal, or C (natural gas) = 100,000 BTU/100 cubic feet

4. TAX CREDIT QUALIFICATION:  Fill out the Tax Credit Qualification Form (see below), demonstrating and certifying that the proposed home uses no more than 50% of the 2004 IECC reference home.

5.  Submit both files and the Tax Credit Qualification Form to AHFC.

<a name="reference-specs"></a>
### Table 1: Specifications for the Standard Reference and Proposed Designs

| **Building Component** | **Reference House File** | **Proposed House File** |
|------------------------|--------------------------|-------------------------|
| Above grade walls      | *Type:* mass wall if proposed wall is mass, otherwise wood frame.  *Gross Area:*  Same as proposed. *Insulation:* R19 | As proposed. |
| Basement/Crawlspace walls| *Type:* same as proposed.  *Gross Area:* same as proposed. *Insulation:* R-10 continuous or R-13 in framing cavity. | As proposed |
| Above grade floors | *Type:* wood frame. *Gross area:* same a proposed. *Insulation:* R-30 | As proposed |                                                                        
| Ceilings           | *Type:* wood frame. *Energy heel:* full depth to exterior walls. *Gross area:* same as proposed. *Insulation:* R-38 | As proposed |    
| Windows (south)    | *U-factor:* 0.35  *Area:* 4.5% of conditioned floor area.  *External shading:* None. | As proposed | 
| Windows (not south) | *U-factor:* 0.35  *Area:* 13.5% of conditioned floor area. *External shading:* None | As proposed |                                                                        
| Skylights                   | none| As proposed|
| Doors   | 40ft<sup>2</sup>, *U-factor:* 0.35| As proposed|
| Air exchange rate           | *Specific Leakage Area (SLA):* 0.00048 with no energy recovery.  *For AKWarm:* **ACH = SLA * 1000 * W * NS**    where W = weather factor (ASHRAE Std. 136, below) and NS = number of stories | As tested |                           
| Mechanical ventilation      | None, unless mechanical ventilation is specified by the proposed design, in which case: **Annual vent fan energy (kWh/yr) = 0.03942 x CFA + 29.565 x (N + 1)**, where CFA = conditioned floor area, and N = number of bedrooms| As proposed |
| Heating systems  | *Fuel type:*same as Proposed Design.  *Efficiencies (use prevailing federal minimum):*                               Electric: air-source heat pump, Non-electric furnaces: AFUE 78%, Non-electric boiler: AFUE 80% | As proposed |                                               
| Thermostat                  | *Type:* manual, *Heating temperature set point:* 68º F | As proposed |
| Heating System Distribution | Choose semi-conditioned space, moderately leaky ducts | As tested |
| Water heater                | *Fuel Type:* Same as proposed design, *Efficiency:* Oil – EF 0.50, Gas – EF 0.57, Electric - EF 0.90 | As proposed |


<a name="tax-credit-faq"></a>
### Tax Credit FAQ (From RESNET website: http://www.natresnet.org)

**Q: Who can qualify for the new homes tax credit?**

**A:** Under the provision for energy efficient homes tax credit, an eligible contractor who constructs a qualified new energy efficient home may qualify for the credit. For specific qualifications to be eligible for the tax credit please consult with a qualified tax advisor.

**Q: Do homes eligible for the Energy Star label also meet the requirements for the tax credit?**

**A:** No. The requirements to meet Energy Star and the tax credit are different. Qualification for Energy Star covers all energy use in a house, including water heating, lighting and appliances, *while requirements for the tax credit only include space heating and cooling.*

**Q: What does an eligible certifier (home energy rater) need to sign and give to the builder for verification for the tax credit?**

**A:** An eligible certifier needs to sign the following statement on every home they are verifying for the tax credit:

“Under penalties of perjury, I declare that I have examined this certification, including accompanying documents, and to the best of my knowledge and belief, the facts presented in support of this certification are true, correct, and complete.”

**Q: What is the time period in which the tax credit can be claimed?**

**A:** To qualify for the credit, homes must be acquired from the eligible contractor after , and before .

**Q: Can a homeowner apply for the tax credit?**

**A:** No, only eligible contractors can apply for the tax credit.

**Q: Can homes be verified for the tax credit using the “sampling” method?**

**A:** Yes. The allows sampling as long as the builder builds at least 85 homes a year and the eligible certifier (home energy rater) follows the current Environmental Protection Agency’s ENERGY Homes Sampling Protocol Guidelines. Of course the certifier must also sign the required statement certifying the home’s compliance.

**Q: Can multi-family homes be eligible for the tax credit?**

**A:** Yes. The defines all homes are eligible for the tax credit as long as the building is not more than three stories above grade in height.

**Q: The rules states that the tax credit is $2,000 per qualifying dwelling unit. How does the define a “dwelling unit”?**

**A:** The defines a dwelling as a “single unit providing complete independent living facilities for one or more persons, including permanent provisions for living, sleeping, eating, cooking and sanitation.”

**Q: Are there any insurance requirements for individuals performing the analysis for the tax credit?**

**A:** Yes. RESNET requires that the rating firm/individual must carry professional liability insurance in the amount of least $500,000 in professional liability. The person who is authorized to bind the company must sign and submit to RESNET the following:

*“Under the penalties of perjury, I declare that \_\_\_\_\_\_\_ carries a minimum of $500,000 in professional liability. I also acknowledge that if a rater inaccurately presents facts in support of the certification of the tax credit it could result up to and including RESNET removing its accreditation as a tax credit certifier.”*

This declaration must be signed and sent to RESNET *prior to the certification of any homes for the tax credit*.

**Q: What’s the difference between a tax credit and tax deduction?**

**A:** Tax deductions reduce tax payer’s overall taxable income with the value of the deduction dependent on the payer’s tax bracket. Tax credits on the other hand reduce the amount of tax a taxpayer owes dollar for dollar. Tax credits are more economically powerful than deductions.
