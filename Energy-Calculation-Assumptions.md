Jim Desrochers

.NET Programmer/Analyst

CCHRC

December 7, 2011

ASSUMPTIONS USED IN THE ENERGY CALC CLASS

OF THE AKWARM CALC PROJECT

*Table of Contents:*

*Methods and Functions* *Page* *Declarations and Constants* *Page*

EnergyCalc.CalcSetbackEffect() 2 EnergyCalc.mLtAppAlloc() 5

EnergyCalc.SetbackDeltaT() 2 EnergyCalc.MASS\_FT2\_STANDARD 9

EnergyCalc.CalcMechVent() 3 EnergyCalc.MASS\_FT2\_HEAVY 10

EnergyCalc.DesignSpaceHeatingLoss() 4 EnergyUtil.HEADER\_FRAC 10

EnergyCalc.SiteWindMult() 4 EnergyUtil.ASSUMED\_WIND 10

EnergyCalc.CalcPeopleGain() 5

EnergyCalc.CalcApplianceEnergy() 5

EnergyCalc.CalcNaturalInfil() 6

DHWheater.CalcEnergyUse() 6

EnergyCalc.CalcLossGr() 8

EnergyCalc.RevisedTemp() 8

EnergyCalc.ThermalMass() 8

EnergyCalc.CalcUseableSolar() 8

EnergyCalc.CalcCoolingLoadAndFuel() 9

EnergyUtil.MovingAirFilmR() 10

EnergyUtil.AirGapR() 11

EnergyUtil.InsulationR() 11

EnergyUtil.OpaqueSHGC() 11

EnergyUtil.WindowSHGCfromGlassSC() 11

EnergyUtil.ModifiedSHGC() 12

EnergyUtil.InterpolatedCost() 12

ShellComponentList.RvalueSummary() 12

ShellComponentList.ShellR() 13

ShellComponent.Calculate() 13

ShellComponent.UA() 13

ShellComponent.MaintenanceCost() 13

HomeInputs.UpgradeVersion() 14

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Method EnergyCalc.<span id="CalcSetbackEffect" class="anchor"></span>CalcSetbackEffect()

This routine calculates the amount that the average daily living space temperature is lowered due to the presence of a night setback thermostat, if one is present.

Assumptions:

Const SETBACK\_DEG As Single = 5.0!

Set Number of degrees F the temperature is assumed to be setback at night. This is only used if ReduceSetbackEffect is not equal to zero.

Assumption Source: User

Const SETBACK\_HRS As Single = 8.0!

Set Number of hours the temperature is assumed to be setback at night.

Assumption Source: User

Dim NightGains As Single = mIntGainGr(mo) \* 0.6!

Estimate the night-time internal gains as 60% of the average value.

Assuming gains are released into living space not cool space, not entirely accurate, but good enough.

Assumption Source: User

Dim NightOutTemp As Single = mWx.DBTemp(mo) - 4.5!

Estimate the night-time outdoor temperature as 4.5 degrees below the daily average temperature.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Method EnergyCalc.<span id="SetbackDeltaT" class="anchor"></span>SetbackDeltaT()

Calculates the average indoor temperature depression caused by a night-time temperature setback. Temperature depression is averaged over the full 24 hours of the day. The morning warm-up period is not considered. The routine assumes the indoor temperature exponentially decays towards the balance temperature of the home.

Assumptions:

Subroutine assumption

> The routine assumes the indoor temperature exponentially decays towards the balance temperature of the home.
>
> Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Method EnergyCalc.<span id="CalcMechVent" class="anchor"></span>CalcMechVent()

Calculates the effects of mechanical ventilation: cfm of flow, amount of heat recovery, and electricity use.

Assumptions:

Const ACH\_MANUAL As Single = 0.29!

> Set Total ventilation (ACH = annual average air change rate for a conditioned space in volume changes per hour) in a house that is tight and has no mechanical ventilation system with HOT-2000 value.
>
> Air is assumed to be added by opening windows.

Assumption Source: Original AkWarm (HOT-2000)

Const ACH\_MANUAL\_IECC As Single = 0.35!

Set Total ventilation (ACH) in house that is tight and has no mechanical ventilation system with IECC 2004 value.

Air is assumed to be added by opening windows.

Assumption Source: IECC 2004 Standard

If VentSystem.VentType = VentilationSystem.VentilationType.None then

ReqdTotalCfm = RelevantVol \* ACH\_MANUAL\_IECC / 60.0!

Else

ReqdTotalCfm = 0.01 \* CondxFloorArea + 7.5 \* (NumBedrooms + 1)

End if

Determine the target total air flow rate, natural + mechanical using IECC 2004 Standard.

Assumption Source: IECC 2004 Standard

Select Case VentSystem.VentType

Case VentilationSystem.VentilationType.None

ReqdTotalCfm = RelevantVol \* ACH\_MANUAL / 60.0!

Case VentilationSystem.VentilationType.Mechancial\_with\_no\_Heat\_Recovery or VentilationSystem.VentilationType.IECC\_Ref\_Mech

ReqdTotalCfm = RelevantVol \* ACH\_NO\_HR / 60.0!

Case VentilationSystem.VentilationType.HRV

ReqdTotalCfm = RelevantVol \* ACH\_HRV / 60.0!

End Select

Determine the target total air flow rate, natural + mechanical using HOT-2000.

Assumption Source: Original AkWarm (HOT-2000)

RelevantInfil = mNatInfil(mo) \* 1.0

mNatInfil(mo) is the monthly Natural Infiltration.

This calculates the Relevant Infiltration value using IECC assumptions.

Assumption Source: IECC 2004 Standard

RelevantInfil = mNatInfil(mo) \* LivingInfilFrac

mNatInfil(mo) is the monthly Natural Infiltration.

LivingInfilFrac is the Fraction of the total infiltration that is in living spaces as opposed to cool spaces (garage).

This calculates the Relevant Infiltration value using HOT-2000 assumptions.

Assumption Source: Original AkWarm (HOT-2000)

RelevantVol = Volume

Determine the volume to apply ACH figures to using IECC assumptions.

Assumption Source: IECC 2004 Standard

RelevantVol = Volume \* LivingVolFrac

LivingVolFrac is the Fraction of the total volume that is in Living spaces, as opposed to in cool spaces (garage).

Determine the volume to apply ACH figures to using HOT-2000 assumptions.

Assumption Source: Original AkWarm (HOT-2000)

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyCalc.<span id="DesignSpaceHeatingLoss" class="anchor"></span>DesignSpaceHeatingLoss()

Returns the space heating demand of the conditioned space (both Living Space and Garage) under design conditions.

Assumptions:

Function Assumption

Assumes all conditioned spaces are at 70 deg F.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyCalc.<span id="SiteWindMult" class="anchor"></span>SiteWindMult()

Get the multiplier factor to convert weather station wind speed to site wind speed, measured at the height of the top floor ceiling.

This function returns the result of the formula: SiteWindMult = Coeff \* (HouseHt/32.8) ^ Expnt.

Assumptions:

Function Assumption

Weather station wind measurement height = 20 feet.

Assumption Source: Ecotope's report "Modeled and Measured Infiltration: A Detailed Case Study of Four Electrically Heated Homes"

In above formula, Coeff = 0.412! and Expnt = 0.25!

Assumptions for the case of HomeInputs.WindShield.Shielded are Terrain Class 4, Shielding Class 4.

Assumption Source: The Lawrence Berkeley Laboratory infiltration model in "The Prediction of Air Infiltration", M. Sherman and B. Dickinson, July 1985, LBL-19040.

In above formula, Coeff = 0.678! and Expnt = 0.2!

Assumptions for the case of HomeInputs.WindShield.Average are Terrain Class 3, Shielding Class 3.

Assumption Source: The Lawrence Berkeley Laboratory infiltration model in "The Prediction of Air Infiltration", M. Sherman and B. Dickinson, July 1985, LBL-19040.

In above formula, Coeff = 0.805! and Expnt = 0.2!

Assumptions for the case of HomeInputs.WindShield.Exposed are Terrain Class 3, Shielding Class 2.

Assumption Source: The Lawrence Berkeley Laboratory infiltration model in "The Prediction of Air Infiltration", M. Sherman and B. Dickinson, July 1985, LBL-19040.

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyCalc.<span id="CalcPeopleGain" class="anchor"></span>CalcPeopleGain()

This routine calculates the average Btu/hour of internal gains produced within the home for each month, using formula PplGain = Occupants \* 174.0!

Assumptions:

Function Assumption

Assumption is that the average sensible heat gain from the average person (mix of male and female adults and children) is 62 Watts. Also, calculation assumes that people are in the building for 82 percent of the time.

Thus the multiplier used in above formula is 62 Watts \* 3.413 Btu/hr/Watt \* 0.82 = 174 Btu/hour.

Assumption Source: “ASHRAE Fundamentals 2009” or “ASHRAY journal of 1983”.

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Declaration EnergyCalc.<span id="mLtAppAlloc" class="anchor"></span>mLtAppAlloc()

Set up allocation factors for allocating other lights/appliance fuel use and gain across the various months in the CalcApplianceEnergy routine. Factors are ratio of that months use to the average months use.

Assumptions:

Declaration Assumption

The dryer and range use is assumed to be evenly distributed.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Method EnergyCalc.<span id="CalcApplianceEnergy" class="anchor"></span>CalcApplianceEnergy()

This routine calculates the fuel use and internal gains from lights and appliances, not including Domestic Hot Water heating, space heating, and mechanical ventilation systems. The fuel and internal gain results are added to the current entries in the annual mAppFuel array, the monthly mFuel array, and monthly mIntGainsGr array.

Assumptions:

To determine internal heat gains, assume 95% of heat gain is released inside of the insulated shell.

The reason that 100% of the heat gain is not released inside of the insulated shell, is that some of it is lost to outdoor lighting, other outdoor use, and light fixtures in the top floor ceiling. Hot-2000 implicitly assumes this because their internal gain utilization curve tops out at 95%.

Assumption Source: Original AkWarm (HOT-2000)

mLtAppAlloc = {0.0, 1.13, 1.075, 1.0, 0.925, 0.87, 0.85, 0.87, 0.925, 1.0, 1.075, 1.13, 1.15}

Factors are ratio of that months use to the average of 12 months fuel use. The dryer and range use is assumed to be evenly distributed over the 12 months.

They were developed from judgment, no hard data to support them.

These factors follow a cosine function with a peak in December.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Method EnergyCalc.CalcNaturalInfil()

This routine calculates the natural infilitration by month and puts the result in the mNatInfil array.

Assumptions:<span id="CalcNaturalInfil" class="anchor"></span>

Subroutine assumption

The STACK and WIND constants are derived from the LBL model using the following, assumptions: R = 0.5, X = 0, and n (the flow exponent) = 0.67.

R and X are not defined, and the equation they are used in is not stated in the comment section. This information needs to be added in order to make sense of this.

Assumption Source: The Lawrence Berkeley Laboratory infiltration model in "The Prediction of Air Infiltration", M. Sherman and B. Dickinson, July 1985, LBL-19040.

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Method DHWheater.<span id="CalcEnergyUse" class="anchor"></span>CalcEnergyUse()

This routine calculates the energy use and contribution to internal gains of the Domestic Hot Water Heating system.

Assumptions:

Dim TankTemp As Single = 120

> Set the Tank Temperature = 120 degrees Fahrenheit if using IECC assumptions.

Assumption Source: IECC 2004 Standard

Dim TankTemp As Single = 135

> Set the Tank Temperature = 135 degrees Fahrenheit if using original AkWarm assumptions.

Assumption Source: Original AkWarm (HOT-2000)

Dim TotalConsump As Single = 30.0 + 10.0 \* NumBedrooms

> Set the TotalConsumption to this value if using IECC assumptions.

Assumption Source: IECC 2004 Standard

Dim TotalConsump As Single = CONSUMP\_PER\_PERSON \* Occupants

> Set the TotalConsumption to this value if using original AkWarm assumptions.

Assumption Source: Original AkWarm (HOT-2000)

Const BLANKET\_FRAC! = 0.9!

Fraction of tank surface area covered by insulating blanket if present.

Assumption Source: User

Const BLANKET\_R! = 6.0!

Assumed R-value of water heater blanket.

Assumption Source: User

Const T\_CONDX! = 71.0!

Average annual temperature of conditioned space.

Assumption Source: User

Const T\_SEMI! = 57.0!

Average annual temperature of semi-conditioned space (deg F)

Assumption Source: User

Const T\_UNCONDX! = 40.0!

Average annual temperature of unconditioned space (deg F)

Assumption Source: User

Const IN\_T! = 45.0!

Inlet water temperature (deg F)

Assumption Source: User

Const CONSUMP\_PER\_PERSON! = 20.0!

Gallons per person per day of hot water consumption (= REM-RATE assumption)

In the comment section it says this constant is not used if using IECC assumptions, but in the code it is used regardless of using IECC or original AkWarm assumptions.

Maybe this is an error in the code or the comment.

Assumption Source: Original AkWarm (HOT-2000)

Function Assumptions.

1) The heat required to raise the temperature of the water flowing through the hot water heater is proportional to the amount of hot water consumption.

2) The conduction of heat is out of the hot water storage tank, if one exists;

3) "Other" heat losses, which include, at a minimum, the lost energy caused by warm air rising up the flue of a gas/oil hot water heater during the off-cycle (NOT counting on-cycle flue loss), thermo siphon heat loss from pipes connecting to the hot water heater (the kind remedied by heat traps), and pilot light loss.

*These three forms of heat load are assumed to be supplied by a heating element or burner operating at a* *particular Recovery Efficiency or steady-state efficiency*.

Heat loads of type 1) and 2) vary from GAMA test conditions to Actual operating conditions, and are adjusted in the actual operating condition calculation.

*The "Other" heat loss, type 3, is assumed to be the same under GAMA conditions and actual conditions*.

Assumption Source: User

ConductLoad = 0.0!

Calculate GAMA conduction load. If there is no tank, assume 0 conduction load.

Assumption Source: User

OtherLoad = FuelUse \* RecovEffic - WaterLoad - ConductLoad

Derive the "Other" load from what's left over after netting out water load and conduction load out of total load.

Now we have the OtherLoad, *which is assumed to remain constant under actual operating conditions*.

Assumption Source: User

If Me.Fuel = EnergyUtil.FuelType.Electric Then

IntGain = FuelUse - WaterLoad

Else

IntGain = 0.5! \* (FuelUse - WaterLoad)

End If

If electric, all loss goes into space.

If fuel-fired, assume half of loss is gain into space around water heater.

Assumption Source: User

IntGain = IntGain + WaterLoad \* 0.03!

As HOT-2000 does, add 3% of the WaterLoad as gain because some heat is lost from the DHW hot water pipes directly into conditioned space.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Method EnergyCalc.<span id="CalcLossGr" class="anchor"></span>CalcLossGr()

Calculate the gross heat loss, without netting out useable internal and solar gains by month and by indoor temperature zone.

Assumptions:

The cool temperature zone setpoint is a constant DEG\_COOL.

There is no setback assumed for this zone.

> No setback is assumed for the DEG\_COOL zone.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyCalc.<span id="RevisedTemp" class="anchor"></span>RevisedTemp()

This routine gets the "Revised Outdoor Temperature" as defined in the Hot-2000 technical manual, version 6, page 2-4.

Assumptions:

StdSqrN = MoStd \* 5.32! ' Assumes 28.25 days for Feb

Uses multiplier in calculation of 5.32 assuming 28.25 days in February.

Assumption Source: Original AkWarm (HOT-2000)

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyCalc.<span id="ThermalMass" class="anchor"></span>ThermalMass()

Get an estimate of the buildings thermal mass for purposes of estimating the utilization of solar gains.

Assumptions:

Function Assumption.

It ignores mass in cool temperature zones, based on the assumption that most solar gains are admitted to the living space, and mass in the cool zones is isolated from the living space.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Method EnergyCalc.<span id="CalcUseableSolar" class="anchor"></span>CalcUseableSolar()

This routine calculates the useable portion of the total solar gains admitted to the building.

Assumptions:

Method Assumption.

This routine estimates gain to load and mass to gain ratios for the living space, not counting cool temperature spaces. The routine implictly assumes the solar gain is primarily admitted to the living space, not the cool

temperature space.

Assumption Source: User

mSolarUtiliz(mo) = (a + b \* GLR) / (1.0! + c \* GLR + d \* GLR \* GLR)

In choosing the coefficients (a, b, c, and d), a compensating assumption made in the routine is that the occupants will allow a temperature swing of 5.5C (9.9F), which is somewhat high.

There are some anomalies in the 2.75C temperature swing curves, primarily noticed weirdness in the Light curve, so the 5.5C curve was used instead.

Assumption Source: User

Method Assumption.

Assume that useable internal gains offset the same percentage of the living space and cool space heat loss. Assumption Source: User

NetGrossLossRatio = (LossGrTot(mo) - mIntGainNet(mo)) / LossGrTot(mo)

The ratio of (loss with useable internal netted out) to (total loss) is calculated for whole building (living + cool), but is assumed to be the same in each separate zone.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Method EnergyCalc.<span id="CalcCoolingLoadAndFuel" class="anchor"></span>CalcCoolingLoadAndFuel()

Calculate the cooling load by month and cooling fuel use. If there is no cooling system, the load and fuel values are set to zero.

Assumptions:

Method Assumption.

Natural cooling, such as open windows and doors, is assumed to cool the building when the outdoor temperature is enough below the cooling setpoint.

Assumption Source: User

Method Assumption.

The constant below determines the minimum number degrees F below the setpoint that outside temperatures

must be to fully cool the building. If the differential shrinks less than this, mechanical cooling is assumed to be needed.

Assumption Source: User

Method Assumption.

Making the assumption cooling only occurs for the areas at Living space temperature, not the Cool temperature. Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Const EnergyCalc.MASS\_FT2\_STANDARD

Mass per square foot for Standard construction, Btu/deg F/ft2.

<span id="MASS_FT2_STANDARD" class="anchor"></span>

Assumptions:

Const MASS\_FT2\_STANDARD As Single = 3.5!

Hot-2000 uses 2.94 for standard frame construction. EEDO uses 1.9 for light 3.8 for medium, and 5.7 for Heavy.

Assumption Source: Original AkWarm (HOT-2000) and EEDO and User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Const EnergyCalc.<span id="MASS_FT2_HEAVY" class="anchor"></span>MASS\_FT2\_HEAVY

Mass per square foot for Heavy construction, Btu/deg F/ft2.

Assumptions:

Const MASS\_FT2\_HEAVY As Single = 7.0!

I (Alan) have found that cool-down data on relatively standard construction implies more like 7 Btu/deg F/ft2.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Const EnergyUtil.<span id="HEADER_FRAC" class="anchor"></span>HEADER\_FRAC

Fraction of wall that is door and window headers.

Assumptions:

Const HEADER\_FRAC As Single = 0.03!

Fraction based on 11.3% window/gross wall ratio 4' high windows and a couple doors per home. Assumes 4x10s used for headers.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Const EnergyUtil.<span id="ASSUMED_WIND" class="anchor"></span>ASSUMED\_WIND

Assumed wind speed for calculating moving air film R-values for components.

Assumptions:

Const ASSUMED\_WIND As Single = 15.0!

Assumed wind speed of 15 mph.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyUtil.<span id="MovingAirFilmR" class="anchor"></span>MovingAirFilmR()

Calculate the Air film resistance for a moving air film given the Air Speed.

Assumptions:

Function Assumption.

It uses a quadratic curve fit equation that is probably inaccurate above 30 mph. The points used to generate the quadratic were: R-0.68 for 0 mph, R-0.25 for 7.5 mph, R-0.17 for 15 mph, R-(1/8) for 25 mph. The points are from Moving Air film tables and a related figure in the ASHRAE Handbook of Fundamentals, 1985. The 25 mph point comes from Fig. 1 Ch 23, 1981 Fundamentals, *assuming Clear Pine*.

Assumption Source: “ASHRAE Fundamentals 1985”

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyUtil.<span id="AirGapR" class="anchor"></span>AirGapR()

This function returns the R-value of an air gap, given its thickness and the direction of heat flow.

Assumptions:

Function Assumption.

Values are determined by interpolation from ASHRAE Fundamentals Air Space R-value tables *assuming an* *effective air space emittance of 0.82, a mean air space temperature of 50F, and an air space temperature* *difference of 10F*.

Assumption Source: “ASHRAE Fundamentals 1985”

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyUtil.InsulationR()

Get the R-value of an insulation layer of a particular thickness.

Assumptions:<span id="InsulationR" class="anchor"></span>

Function Assumption.

Assumes a horizontal air gap if the insulation is missing or if there is no insulation ID.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyUtil.<span id="OpaqueSHGC" class="anchor"></span>OpaqueSHGC()

This function returns the Solar Heat Gain Coefficient, ratio of solar heat admitted into the building to the solar energy incident on the surface, of an opaque shell component.

Assumptions:

Const ABSORB\_ORIGINAL = 0.4

Assumed solar absorptances of the outer surface of the component, using HOT-2000 standard.

Assumption Source: Original AkWarm (HOT-2000)

Const ABSORB\_IECC\_2004 = 0.75

Assumed solar absorptances of the outer surface of the component, using IECC 2004 standard.

Assumption Source: Original IECC 2004 Standard

Const ASSUMED\_WIND As Single = 15.0!

Assumed wind speed for calculating moving air film R-values for components.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyUtil.WindowSHGCfromGlassSC()

Converts a glass shading coefficient into a window Solar Heat Gain Coefficienct (SHGC).

Assumptions:

Function Assumption.<span id="WindowSHGCfromGlassSC" class="anchor"></span>

The window frame has a different SHGC than the window. The two sections must be averaged together. *Assumed a NFRC size AA window with a wood frame.*

Assumption Source: “ASHRAE Fundamentals 1993”

Function Assumption.

Shading external to the building (for example, trees, neighboring buildings, mountains) is NOT accounted for in this function. Dirt on the glazing is not accounted for.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyUtil.<span id="ModifiedSHGC" class="anchor"></span>ModifiedSHGC()

Get the Solar Heat Gain Coefficienct (SHGC) of a window that has additional glazing added to it, such as a storm window.

Uses the Shading Coefficient (SC) of the glass.

Assumptions:

Function Assumption.

*Assumes* a reasonable approximation for the new SHGC of the glass only is SHGCinit \* SHGCaddition.

SHGCaddition is not defined anywhere in the program, so not sure what this assumption really means.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function EnergyUtil.<span id="InterpolatedCost" class="anchor"></span>InterpolatedCost()

Returns an interpolated cost. Used to interpolate Library costs between the cost for a Low Cost city (CityCostLevel=1) and the cost for a High Cost city (CityCostLevel=5).

Assumptions:

Function Assumption.

Interpolate between low and high costs based on city cost level.

*Assume each level is an equal percentage above the prior level*.

There are 4 increases from level 1 to level 5.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function ShellComponentList.<span id="RvalueSummary" class="anchor"></span>RvalueSummary()

This routine calculates the average R-value (actually 1 / average U-value for each type general type of shell component, such as floors, walls, and doors, including the effects of ground in contact with any of the components.

Assumptions:

Function Assumption.

This routine assumes that the Calculate() method on this ShellComponentList has already been called. Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function ShellComponentList.<span id="ShellR" class="anchor"></span>ShellR()

Returns the average R-value (acutally 1 / average-U) for shell component types present in a list. U-values of cool temperature components (garage) are downweighted.

Assumptions:

If sh.Temp = IndoorTemp.Living\_Space Then

UAtot += sh.UA(EnergyUtil.ASSUMED\_WIND)

Uses assumed heating wind speed as opposed to actual for shell R-values.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function ShellComponent.<span id="Calculate" class="anchor"></span>Calculate()

Called to update the R-values of the component.

Assumptions:

Me.Output.SHGC = Me.SHGC(EnergyUtil.ASSUMED\_WIND)

Approximate because using Assumed wind speed.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function ShellComponent.<span id="UA" class="anchor"></span>UA()

Returns the Unit Area (UA) value of this component, adjusted for a different surface wind speed if RaffectedByWind is True. Calculate() method must be called prior to this routine.

Assumptions:

Radj = EnergyUtil.MovingAirFilmR(SurfaceWind) - EnergyUtil.MovingAirFilmR(EnergyUtil.ASSUMED\_WIND)

Approximate because using Assumed wind speed.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Function ShellComponent.<span id="MaintenanceCost" class="anchor"></span>MaintenanceCost()

Return the annual maintenance cost of the improvement, in $ per year.

Assumptions:

Function Assumption.

Maintenance cost is ratioed off of the installation cost, however do not consider the user Cost Adjustment as that is assumed to only apply to the initial cost.

Assumption Source: User

Function Assumption.

Do It Yourself (DIY) adjustment \*is\* assumed to apply to the maintenance cost since an owner who installs the measure themselves will probably do some of the maintenance.

Assumption Source: User

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Method HomeInputs.UpgradeVersion()

Updates properties that weren't present in old versions of this class.

Assumptions:

<span id="UpgradeVersion" class="anchor"></span>

blw.IsCrawlWall = IIf(blw.WallHeight \< 6.0, True, False)

If average wall height is less than 6 feet, then assume this is a crawl-space wall.

Assumption Source: User

GarageFloorArea

Estimate the floor area of the conditioned garage.

Estimate as 4.03 times the total area of entered garage doors.

Factor is from 22' x 21' garage with 16' x 7.16' garage door.

Assumption Source: User
