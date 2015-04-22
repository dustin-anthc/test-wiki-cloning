ENERGY RATING PROGRAM EVALUATION
================================

## Contents

1.  [[Introduction|Rating-Program-Evaluation#eval-intro]]

2.  [[Scope of Work|Rating-Program-Evaluation#scope-of-work]]

3.  [[User Requirements|Rating-Program-Evaluation#user-requirements]]

4.  [[Desired Features|Rating-Program-Evaluation#desired-features]]

5.  [[Energy Modeling Methods|Rating-Program-Evaluation#modeling-methods]]

6.  [[Home Energy Rating System Points|Rating-Program-Evaluation#point-issues]]

7.  [[Software Packages Reviewed|Rating-Program-Evaluation#software-packages]]

8.  [[Options and Costs|Rating-Program-Evaluation#options-and-costs]]


### [Appendices](/..wiki/Images/Energy-Rating-Program-Evaluation-Appendices.pdf)

A. Energy Use Software Program Information

B. EnergyGauge

C. REM/RATE

D. TREAT

E. Comparing Simulation Engines

F. Summary of Comments from HERS Users & Providers

G. IRS Energy Efficient Home Credit IRC Section 45L and List of Eligible Software Programs for Certification

<a name="eval-intro"></a>
## Introduction

This project is presented to the Cold Climate Housing Research Center (CCHRC) by the Alaska Building Science Network (ABSN). Its purpose is to assist CCHRC in its advisory relationship with the Alaska Housing Finance Corporation (AFHC) to decide the best course of action with regards to choosing a software package for AHFC’s Home Energy Program. The project was authorized by CCHRC contract number 2007-04 for AKWarm Program Evaluation.

Since 1995 AFHC’s Home Energy Rating Program has used the locally developed AKWarm software which, when it was written it was on the cutting edge of energy analysis software. Besides being easy to learn, it was capable of providing outputs for a variety of users and purposes including residential building energy load calculations, weatherization retrofit economics, energy ratings, energy-efficient mortgages, and compliance testing for ’s Building Energy Efficiency Standard (BEES). It tested remarkably well against the more robust DOE2 energy modeling program and was approved by secondary lenders and the EPA Energy Star program. AkWarm was designed for a Windows-based computer with a “386” microprocessor and 5 MB of free disk space. In the intervening years, while the Microsoft operating systems have changed numerous times, AkWarm has been virtually error-free and has been used to perform over 25,000 energy ratings and energy use simulations. While there have been a number of attempts to update the program, the version 1.03d that was put in place in 1995 is still being used today with no significant changes other than the in the database libraries. Meanwhile there have been a number of changes in the world of residential energy programs:

-   In 2002 a national non-profit organization, Residential Energy Services Network (RESNET), was incorporated to develop national standards for home energy ratings. RESNET has also developed a program for certifying energy rating tools, including performance compliance software programs and rater training programs. RESNET has been an integral part of the development of the Federal government’s residential energy rating and tax credit programs. *Neither AkWarm nor AHFC’s Home Energy Rating Program have been certified by RESNET*.

-   In July 2005 Congress passed the 2005 Energy Policy Act. The legislation provided for a $2000 tax credit to builders for building energy efficient homes. To meet the tax credit requirements, a home must use no more than 50% of the energy used by a home built to 2004 International Energy Conservation Code (IECC) standards. The only way to determine if a home will qualify for the tax credit is to have an analysis done using one of the approved IRS software programs. Software approval must be provided by RESNET or “an equivalent rating network”. *AkWarm has not yet been approved for tax credit certification by any agency*.

-   On November 8, 2006, BEES 1991 was replaced (with the adoption by reference in 15 AAC 155.010) by BEES-2007, which includes the residential provisions of the 2006 IECC, ANSI/ASHRAE Standard 62.2-2004, and Alaska-specific amendments to both of those documents. The standard update became effective on . In order to continue to use AkWarm for showing compliance AHFC’s BEES-2007, the AkWarm reference home library must be recalibrated to create a reference house that meets this new set of criteria. *Currently new homes with foundations poured on or after are not in compliance if they rely on the Four Star Plus (83 point) AKWarm energy rating.*

-   Since the initial development of AkWarm, personal computers and the range of programs they can support have made it possible to take advantage of more complex energy simulations, and to provide a wider array of output reports. While AkWarm focused on the home’s thermal energy use, today’s home energy analysis programs can also evaluate lighting and appliances, indoor air quality, “green-ness”, and provide room-by-room heating and ventilation designs. This is especially important for Energy Star certified homes and homes seeking certification under a green building standard. In the past, AKWarm Five Star homes were automatically considered to meet the EPA’s Energy Star requirements. However, those requirements changed significantly in July 2006 and now include lighting and appliance elements. *AKWarm Five Star homes no longer meet Energy Star requirements.*

-   The trend for some Home Energy Rating programs (and part of the new RESNET standard) has changed from a zero to 100 point scale where the upper end reflects the most efficient homes to a scale where zero points represent a zero-energy use home. The goal then is to get as close to zero points as possible. With the new system higher points represent excessive energy use. Most of the newer energy rating programs are keyed to this new standard. There is certainly controversy about which method is better, but the direction seems to be toward the new system. *AKWarm is still based on a zero to 100 point scale.*

-   Changes in the Microsoft Windows operating system have occurred many times over the last decade or so. AKWarm has weathered these changes without harm and has functioned well through the current Windows XL systems. This may not be the case with Microsoft’s newest operating system – Windows Vista. It appears that no one has yet been successful getting AKWarm to work with Windows Vista. This is not only an issue for current uses but also for access to the thousands of archived AKWarm ratings. *As users upgrade their computer systems to Windows AKWarm will no longer be functional.*

-   The library that is used in AKWarm was created in an antique version of Microsoft Access (2.0). It will only operate and it can only be modified using that version. There may only be one computer in that still has this version operating! Later versions of Access do not work with AKWarm. *The AKWarm library structure needs to be brought into the 21<sup>st</sup> century.*

Clearly, the time has come for change. The question at hand is: should the State of Alaska move forward with updating and enhancing AkWarm or would it be more economically and logistically feasible to adapt one of the currently certified programs to meet Alaska’s needs in terms of BEES-2007 compliance, Federal tax credits, and other institutional requirements. Our task will be to perform the research and examination necessary to help CCHRC and AHFC make this decision.

Principal work on this project was done by Ginny Moore of Flattop Technical Services (345-1355; <tgmoore@gci.net>) and Geoff Feiler of Heat Loss Analysis (563-0773; <hla@alaska.net>) . Questions regarding this project can be addressed to them directly or via the ABSN office (562-9927; <absn@alaska.net>).

<a name="scope-of-work"></a>
## Scope of Work

In the original proposal presented to CCHRC, ABSN outlined six task areas including:

-   *Characterizing the existing AKWarm software* which involved identifying the existing users and uses of AKWarm. This was accomplished in part by reviewing previous comments made by the largest user group - AHFC Energy Raters – and by relying on the expertise of the researchers who have been involved with ’s energy rating programs since their inceptions. The second significant user group – weatherization providers – was also interviewed to identify their needs and collect their recommendations.

-   *Defining necessary and desirable changes to the AKWarm software* has been given replaced with a more general effort to define a list of features that should be available in any software package chosen to represent AHFC’s program. We already have several lists of desirable AKWarm improvements that have been developed over the last twelve years.

-   *Creating a matrix of specifications* was initially intended to provide a way to compare and possibly rank five or six packages. The matrix was developed early in the project and submitted to CCHRC for review and comment. As research into the available programs progressed, it has become obvious that some of the options do not have what we considered to be minimum feature requirements. Therefore the final review may contain only two or three programs.

-   *Determining which software programs to evaluate* was a rather simple task since the number of available programs is quite limited. For tax credit purposes, the software must be approved by RESNET or an equivalent rating network. Review of other potential packages was requested either by CCHRC or selected based on the researcher’s knowledge of them.

-   *Evaluating AKWarm and other programs* has required the bulk of the effort. We have not needed to evaluate AKWarm because we are intimately familiar with its capabilities and shortcomings. We only need to report them. The other programs have required extensive review to determine if they can be made appropriate for , if they will provide the required features, if there is adequate support, and if the costs are reasonable.

-   *Summarizing and presenting courses of action* is the primary function of this report. We may present more than one course several of which will not be mutually exclusive. We will also present another issue that needs to be resolved with respect to the federal tax credits. This is an action that is independent of the software research but, if it is not resolved, the software selection will be moot as far as tax credits go.

The bulk of the work on this project did not necessarily follow the initially proposed scope. It became evident early on that there were only a few programs that could meet our needs and that some of them did not, at this time, meet all the basic requirements. Early on we determined that the most useful software programs to evaluate for this project were REM/Rate, EnergyGauge, TREAT, and HOT2000/3000.

<a name="program-requirements"></a>
##  Energy Program Requirements

There are basic functions an energy software modeling program must provide in order to meet the requirements of the current AKWarm user groups. They are as follows:

-   *Energy ratings for BEES compliance*: the package must be able to create a reference home based on the 2006 International Energy Conservation Code and the amendments to that code and then compare that reference home to a model based on the actual building elements. The actual home must achieve a Four Star Plus energy rating which begins at 83 points on a zero to 100 point scale, unless we decide to change our general view of the point/star relationship. *Currently AKWarm is the only software package that meets that requirement.*

-   *Energy ratings for AHFC’s Interest Rate Reduction program*: currently homebuyers can get mortgage interest rate reductions (IRRs) by purchasing homes that either meet 5 Star/5 Star Plus requirements or that can be upgraded to show improvements in the energy rating system. In the latter case ratings are performed before and after improvements and the difference between the two determines amount of the rate reduction. *AKWarm is used for these purposes and other packages with improvement analysis capabilities should work as well but minor changes to AHFC’s mortgage guidelines may be necessary*.

-   *Improvement Options Reports (IOR)*: these are essential for some AHFC’s IRRs programs. They outline the improvements that can be made to a home so that the owners can evaluate their options. The reports present the upgrade items in order of cost-effectiveness. The IOR is also used by homeowners who just want ideas on how to make their homes more efficient even if they are not participating in an IRR program.

  - Besides homeowners and homebuyers, the IOR is used heavily by ’s Low-Income Weatherization providers. AKWarm has long been an important tool for these organizations and the IOR helps them prioritize their weatherization tasks. *Improvement option reports are offered by AKWarm, RemRate, and TREAT.*

-   *Design heating load calculations*: these are necessary for sizing heating systems in both new construction and retrofit situations. AKWarm is used by energy raters, architects, building designers, and others to perform this task. *All the software packages can do this but they do not all use the same climate data or calculation methods to achieve their results.*

-   *Federal energy tax credit certification*: as mentioned in the introduction, a $2000 Federal tax credit is available to builders who construct homes that are theoretically 50% more efficient the 2004 amendments to the 2003 International Energy Conservation Code (IECC). Of the five software packages reviewed only two (RemRate and Energy Gauge) are currently approved by RESNET for tax credit purposes. TREAT has been submitted to RESNET for review. AKWarm has been denied approval and that denial is being appealed. HOT3000 is not yet far enough along to be submitted.

  - A critical issue here is the perceived requirement that the software for the tax credits must be approved by RESNET. The IRS regulations actually give the options of approval as “by RESNET (or an equivalent rater network)”. This also holds true for the energy raters themselves. *The selection of a software package for energy rating program is moot if the persons performing the ratings are not also certified by RESNET or “an equivalent rating network”.*
  So what is an “equivalent rating network”? The Alaska Building Science Network has managed to contact the IRS attorney who actually wrote the regulation. So far there is no answer. This attorney has passed the question on to her superiors but has said to not expect an answer until maybe October.

-   *Customer and software support*: this is a critical element for any software package. Not only do the users need to supported, but the software itself should be continuously reviewed, updated, and improved. The support systems for RemRate and TREAT appear to be first-rate, possibly a bit less so for Energy Gauge. HOT3000, being a small part of a large government organization, even less (it took about five phone calls to even find someone who knew about the program). For AKWarm, there have been regular library updates as well as customer support on usage issues, but no effective efforts at keeping the package current.

<a name="desired-features"></a>
## User Desired Features

For a full service package, failure to meet all of the Alaska Energy Program Requirements should mean automatic removal from consideration unless those deficiencies are soon to be corrected. Beyond those elements there are a wide range of features, the inclusion of which can make a program more desirable. Some of the more important are:

-   *User friendliness*: AKWarm is noted for this. Most of the other programs require a far greater number of inputs including walls by orientation and windows by size, wall association and placement on a wall. However, despite require greater detail in some areas, they are less flexible than AKWarm in others.

-   *Flexible and useful report capabilities*: Akwarm produces only a couple reports. All of the other packages provide (or will provide in pending versions) a wide variety of outputs including energy ratings, tax credit compliance reports, proper input reflections, VA/FHA requirements, and a variety of code compliance options. With some, the user can custom-create reports.

-   *Broad weather database:* AKWarm has monthly average weather data for nearly all communities in . Other programs use 30-year average TMY data which is currently available for only 19 locations. If another program is chosen it would be good to find a way to simulate the rest of ’s communities in the TMY structure.

-   *Rating provider library & library support*: All of the programs have non-editable libraries for building components and some other features. They initially appear to be less detailed than AKWarm’s libraries. We would need to be able to add items to these databases without relying on the software provider. Also the AKWarm library is maintained by one person who is rapidly approaching senility in a database that can often be found in antique stores. A new system is essential.

-   *User-definable library*: Letting users create “unofficial” libraries is advantageous because it helps deal with items that don’t show up in the provider library. Currently, the AKWarm library is only updated once a year. User inputs could be useful in maintaining a list of future “official” library needs

-   *Ability to export house files*: This is essential for training and monitoring purposes. All of the reviewed packages have this capability even if their main file system is in a database rather than discrete house files.

-   *Ability to run more than one house at a time*: Users can only have one instance of AKWarm running on their computer at a time. The same holds for Energy Gauge. It would be nice to not have to close one house file in order to work on another.

<a name="modeling-methods"></a>
## Energy Modeling Methods

Many of the energy modeling/energy rating packages currently available use some type of third-party calculation engine. These are generally developed by government energy departments or large research organizations. The software the user buys is just a privately developed interface between the user and the calculation engine. The more common calculation engines are:

-   *DOE2*: Developed in part by Lawrence Berkeley Laboratories (LBL), DOE-2 is a widely used and accepted freeware building energy analysis program that can predict the energy use and cost for all types of buildings. It uses a description of the building layout, construction components, operating schedules, conditioning systems, and utility rates along with weather data, to perform hourly building energy simulations and to estimate utility bills. The “plain” DOE-2 program is a “DOS box” or “batch” program which requires substantial experience to learn to use effectively while offering researchers and experts significant flexibility. DOE-2 is difficult to modify and is no longer supported by the U.S. Department of Energy. DOE-2 is used by Energy Gauge.

-   *EnergyPlus*: EnergyPlus models heating, cooling, lighting, ventilating, and other energy flows as well as water in buildings. While originally based on the most popular features and capabilities of DOE-2 and BLAST (an older simulation engine), EnergyPlus includes many innovative simulation capabilities such as time steps of less than an hour, modular systems and plant integrated with heat balance-based zone simulation, multizone air flow, thermal comfort, water use, natural ventilation, and photovoltaic systems. It is replacing DOE2 as the Department of Energy’s supported calculation engine but is complex and probably more appropriate for commercial building applications. It is not used by any of the reviewed rating software, but an upcoming version of TREAT may change that.

-   *SUNREL*: Created by the National Renewable Energy Laboratory (NREL), SUNREL is a also an hourly building energy simulation program that aids in the design of small energy-efficient buildings where the loads are dominated by the dynamic interactions between the building's envelope, its environment, and its occupants. The program is based on fundamental models of physical behavior and includes algorithms specifically for passive technologies, such as Trombe walls, programmable window shading, advanced glazings, and natural ventilation. In addition, a simple graphical interface aids in creating input files. SUNREL is relatively easy to modify, but changes must be done by NREL. It also has limited mechanical systems analysis capability. SUNREL is used by TREAT.

-   *ESP-r*: ESP-r was developed by the in and is an integrated modeling tool for the simulation of the thermal, visual and acoustic performance of buildings and the assessment of the energy use and gaseous emissions associated with the environmental control systems and construction materials. The system is equipped to model heat, air, moisture and electrical power flows at user determined resolution. The system is designed for the Unix operating system, with supported implementations for Solaris and Linux, and can operate under Windows. It is complex and also difficult to modify. ESP-r is used by HOT3000.

Besides the simulation engines noted above there are programs such as AKWarm, Micropas (used in ) and REM/RATE which use a correlation method for energy load calculations. In these programs there is not a separate calculation engine, the user interface, libraries, calculations, and outputs were developed symbiotically. There is at least one opinion that this type of modeling program is becoming obsolete because the power available in current computer technology make the more complex simulation programs easy to run.

<a name="point-issues"></a>
## Home Energy Rating System Point Issues

Historically, energy rating scores have been on a 0 to 100 point scale with the upper end representing a home with minimal energy use. The lower end has been an arbitrarily determined level of energy use as a function of a reference home which matches the prescriptive requirements of an energy standard. The national HERS reference home is 80 points on the 0 to 100 scale (4 star). A rated home with the same annual energy requirements as its associated reference home would also score 80 points (houses rated at 80 points are also deemed to meet the requirements of the now defunct Model Energy Code). The old EPA Energy Star Homes program required a HERS score of 86 (5 star) to qualify. The HERS reference spread is as follows:

| **HERS Score** | **Stars** | **Energy Consumption**    |
|----------------|-----------|---------------------------|
| 0 to \<40      | 1         | \> 3.0x Reference Home    |
| 40 to \<60     | 2         | \> 2.0x to 3.0x Ref. Home |
| 60 to \<80     | 3         | \> 1.0x to 2.0x Ref. Home |
| 80 to \<86     | 4         | \> 0.7x to 1.0x Ref. Home |
| 86 to \<92     | 5         | \> 0.4x to 0.7x Ref. Home |
| 92 to 100      | 5+        | 0.0x to 0.4x Ref. Home    |

Until recently, the reference home for has been based on the 1992 Building Energy Efficiency Standard and was pegged at 83 points (Four Star Plus). The new standard is to be based on the 2006 IECC with amendments but still pegged at 83 points.

Beginning in 2006 the national HERS index changed from a 0 – 100 point scale to a 0 to 500 points scale with the lower end representing a zero-energy home. The upper end heads toward infinite energy use. The HERS reference home is 100 points on the indexing scale. A rated home with the same annual energy requirements as its associated reference home would also have an index of 100 points. The number of points one receives is the same as the relative amount of energy use. The lower the energy use the lower the rating points with the ultimate goal being zero points.

For HERS 2006 ratings indexes and star ratings correspond as follows:

| **Energy Use Relative to Index** | **Star Rating** |
|----------------------------------|-----------------|
| \<500% and \>400%                | 1               |
| =\<400% and \>300%               | 1+              |
| =\<300% and \>250%               | 2               |
| =\<250% and \>200%               | 2+              |
| =\<200% and \>150%               | 3               |
| =\<150% and \>0%                 | 3+              |
| =\<0% and \>-15%                 | 4               |
| =\<-15% and \>-30%               | 4+              |
| =\<-30% and \>-50%               | 5               |
| =\<-50% and \>=-100%             | 5+              |

<a name="software-packages"></a>
## Software Packages Reviewed

After an exhaustive search on our own, we determined that the most useful software programs to evaluate for this project were REM/, EnergyGauge, TREAT, and 2000/3000.

We contacted others who are involved in energy rating software program evaluation and they agreed that our list was complete:

1.  Advanced Energy, in , looked at nine different programs for a comparison study, before narrowing it down to three programs. REM/Rate, TREAT and EnergyGauge were their winners with regard to ease of use and having the ability to predict different energy use with different foundation setups.  The others were either much more cumbersome or predicted the same energy use regardless of the changing foundation characteristics, or were specific to one location, e.g. . 

2.  Ron Judkoff, Director of Buildings & Thermal Systems Center at the National Renewable Energy Laboratory in Golden, agreed that we were evaluating all of the useful programs. He did summarize his perceptions of the pros and cons of each program (note: he is a co-author of SUNREL, the simulation engine that is “under the hood” of TREAT).

A major effort was made to research the existing software packages that could be potential candidates for adoption by ’s energy programs. There was consistent agreement among developers and users nationwide that the programs that should be considered could be narrowed to:

1.  **REM/Rate v12.4**: REM/Rate is based on heat balance equations modified by correlations. It is not a true simulation, and has difficulty dealing with dynamic heat or mass transfer phenomena that take place in short time increments. It will be less flexible to handle future technology than the true simulation programs.

2.  **EnergyGauge® USA Version 2.6**:  EnergyGauge is based on DOE 2 which is based on a transfer function and weighting factor mathematical approach to solving the heat transfer equations. DOE-2 is no longer supported by the USDOE. It is difficult to modify. EnergyGauge has used the "External Function" capability of DOE-2 to add some features, but the kinds of features that can be added that way is fairly limited.

3.  **TREAT**:  TREAT is based on SUNREL which is based on a numerical (forward finite differencing) approach. SUNREL has limited mechanical systems, but is relatively easy to add new features to. It does a very good job calculating building loads. TREAT provides a user friendly interface. SUNREL has a clearly written Users Manual. The program can be obtained or licensed as TREAT (with the interface) or as SUNREL alone with a less elaborate user interface. Changes to the SUNREL internal code have to be arranged through NREL.

Both REM/Rate and EnergyGauge are certified for use in HERS programs and for use in applying for federal tax credits. TREAT is not currently certified but its developers believe that they will be able to meet those requirements in the near future. Also, the underlying simulation software in EnergyGauge (DOE-2), TREAT (SUNREL), and -3000 have all been tested with the NREL/IEA BESTEST method and have all come out well in those tests. REM- is a correlation method, not a real simulation program and has done well in the NREL/HERS-BESTEST tests, but cannot perform the NREL/IEA BESTEST or ASHRAE Standard 140 tests (based on NREL/IEA BESTEST).

Several other programs were also considered and rejected for this study for various reasons:

1.  **HOT3000**: Hot3000 is a product of the CANMET Energy Technology Centre (part of the Canadian government Natural Resources department). This will be the followup to the well-known HOT2000 program that some Alaskans used many years ago. It is being developed for the Canadian residential market and their models could be more closely compared to Alaskan building construction. However, HOT3000 is not certified for HERS, IECC, Energy Star, or tax credits. It is only in beta version at this time and test runs frequently crashed.

2.  ***EnergyPlus***: EnergyPlus can be used directly as well as a calculation engine for other user interfaces. It was not included in our review because it is a more complex program than necessary for our needs. For a typical home file there may be over 2000 inputs required. Compared to the 100-200 inputs most of the other applications require, this application is exceptionally cumbersome. To give an example of the detail level, the inputs include the need to geometrically determine and input every vertex of the walls, doors, and windows. The outputs of EnergyPlus are also complex and do not include HERS, Energy Star, tax credit, or IECC results.

3.  **BUILDER ENERGY SOLUTIONS CALCULATOR:** This is a package produced by Owens Corning has also been approved as a software tool to serve the interests of the builder looking to take advantage of the $2000 tax credit for each certified home. While this program could help us with access to the tax credits it would not be as useful for other programs such as energy ratings or weatherization.

Our initial intention was to develop several building models that represented Alaskan residential buildings and that we could use for comparison of the 3 software packages and AKWarm. We came up with 4 models: single family building on crawlspace, basement, zero-lot line, and multifamily building that could be moved to different locations in the state.

After a short introductory walk through of each program, we attempted, alone and together, to input the building information into each program. From the very beginning we realized how difficult this would be. There is a great difference among programs in terms of building inputs and some of those differences can affect outputs.

All researchers and developers we talked to agreed that it can be very challenging to develop models that are the same in various software tools.  Developers for RemRate and EnergyGauge who know the intricacies of their own programs, have attempted this many times over the years and told us: “Even for us it is challenging to build models that are truly comparable, and it often takes numerous iterations before we end up with comparable models.” Another study of Energy Star homes in the concluded that:

> *“the researchers determined that the modeling softwares each assess the energy impact of ventilation in different ways. Further research is needed to determine the extent of these variations, and how they may have an impact on results generated by these softwares, including qualification for tax credits.”*

The Residential Energy Services Network's (RESNET) website lists 78 organizations that that have been accredited through the Mortgage Industry National Home Energy Rating System Accreditation Standard. The systems have been reviewed by either the state energy office or Fannie Mae and Freddie Mac and accredited by the Mortgage Industry Accreditation Review Committee.

Accredited rating providers have the responsibility of ensuring the quality of rating services. Rating providers are responsible for administering rating programs. These responsibilities include:

-   Certification of raters

-   Selection of accredited rating software programs

-   Rating quality assurance

-   Marketing of rating services

We contacted all of these organizations that appeared to be involved in programs similar to the rating program provided by AHFC. We asked them to answer a few questions:

1. What software program you use

2. How you use it for your particular programs, and

3. How or if you would change it?

The responses we received were almost all from REM/Rate users. While there are always improvements people would like to see, responders invariably gave REM/Rate high marks for user friendliness and especially for customer support. NO complained about the service they received, which is significant, since REM/ requires ongoing financial costs both to provider and rater.

The consensus was that the program was useful for ratings but that it shouldn’t be considered a load calc program. Internal calculations seem to favor larger homes being able to meet Energy Star levels better than smaller homes. This, however, may be appropriate. Larger homes are inherently more efficient on a BTU/SF basis than smaller homes due to their smaller surface to volume ratio.

NOTE: TREAT and 2000/3000 are not RESNET-certified rating programs so the list of certified providers does would not include those who use their programs. There are some users of EnergyGauge on the list but we received no responses from them.

There were interesting comments about deciding how much we want to be involved in software development as opposed to letting the developers keep up with that and working more on program development and field work to help builders improve their product. Oregon Energy Office also believed that prescriptive energy codes were much more successful than performance based codes that rely on software outputs. The individual responses are provided in the appendix.

It was beyond the scope of this short study to spend additional time on attempting to consistently model the buildings across all software platforms. Since all of them have been independently tested and certified to meet rating and tax program requirements nationwide, we accepted that we were not in a position to second guess the experts.

We then decided to examine each program on its own merits and our “feel” for how well it would meet the needs of our programs and users. Appendix B provides more detailed comments.

Both REM/Rate and EnergyGauge are certified for use in HERS programs and for use in applying for federal tax credits. TREAT is not currently certified but its developers believe that they will be able to meet those requirements in the near future.

<a name="options-and-costs"></a>
## Options and Costs

Before delving into the options for the future of AHFC’s Home Energy Rating Program the authors feel it is necessary to restate two critical facts:

1.  AKWarm, as it is currently used, does not show compliance with the Building Energy Efficiency Standard as it was modified effective . This is a serious problem because homes started after that date are being completed and are in need of a compliance method. Also, plans are now being reviewed for future homes and the official “tool” for this review is not in compliance. *The AKWarm reference home needs to be updated immediately.*

2.  As far as the tax credits go, it does not matter what AHFC does with respect to its software choice. Unless the raters themselves are certified by either RESNET or “an equivalent rating network” builders in will not have access to the tax credits anyway. *AHFC needs to take whatever steps are necessary to either become certified through RESNET or to become recognized as an “equivalent rating network”.*

In the following paragraphs we present potential courses of action, note whether they are long-term or short-term solutions, estimate their production times, and provide rough cost estimates. It should be noted that in most cases there will need to be extensive training for the rater network over and above the times and costs shown in this report. The cost estimates also do not include administrative costs should the development or services be funneled through a third party such as CCHRC or ABSN.


#### Option A: Create an external tax credit analysis routine for AKWarm

It is possible to use the information contained in the AKWarm file and produce new reports with some additional calculations that build on the AKWarm calculation.  An Energy Tax Credit report in this fashion, but the algorithm for compliance would *not* involve simulating an IECC reference house and then comparing it to the AKWarm house.  Compliance would have to be done via a simple algorithm like comparing the Rating Points total to a compliance rating point threshold (e.g. compliance for a single story on crawl house in Anchorage requires a rating point total of 86 or higher).  

**Pros**:

-   Short term solution

-   Local development and support

**Cons**:

-   Would still need to be approved by RESNET (or an equivalent……)

-   Does not address any of the long-term issues

**Cost**: about $15,000

**Timeframe**: 3 months

**Comment**: Probably not worthwhile unless we can be assured of approval

#### Option B: Major Rewrite of AkWarm For Long-Term Needs

When AKWarm was originally developed, it used a number of third party add-ons to the Visual Basic 3.0 programming language. Most of those add-ons are no longer available, no longer supported, and no longer needed. To become current with existing needs and provide for the future a number of major changes would be necessary including:

-   Rewrite software into VB.Net. This requires incorporating previous add-ons directly into the new version, making other necessary software changes, and recompiling the entire package. This step basically gives us AKWarm as we have it now without any improvements other than being able to run on Windows Vista. It is, however, necessary before any other improvements can be implemented. At this stage we might even consider using one of the simulation engines instead of a correlation method.

-   Make the needed and desired improvements to the VB.Net version of AKWarm:

    -   Review of Assumptions

    -   Improved reporting capabilities

    -   New library format and access regulation

    -   Improvement Options enhancement

    -   Lighting and Appliance module

    -   Alternative Energy module

    -   BEES certification

    -   Tax credit certification

    -   Ventilation certification

    -   Fuel switching options

    -   certification

**Pros**:

-   Can continue to be free to full range of users

-   Local development and maintenance

-   More control over getting just what we want (AKWarm has some input flexibilities not available in the other programs such as multiple insulation levels in a single building element).

-   Minimal training for users

-   Already proven and accepted by state agencies

-   Would allow future flexibility

**Cons**:

-   Would still need to be approved by RESNET (or an equivalent……)

-   Would require a level of future support not presently available from AHFC

-   There is only one developer familiar enough with AKWarm to trust with the new software development

**Cost**: about $50,000 to convert to VB.Net. Probably another $50,000 - $75,000 to make other improvements.

**Timeframe**: 1 year

**Comment**: An exciting prospect but with high cost (although not high relative to AHFC’s previously unsuccessful efforts) and long time frame.

#### Option C. Adoption of nationally-approved software package

The adoption of a nationally approved software package as the basis for showing compliance with the state’s energy standard, as well as being certified for HERS and federal tax credit compliance, has large potential benefits for . While having a unique state program has the benefit of maintaining state control and provides for innovation, it also carries large costs since all supporting documents, training information, and technical interpretations have to be created and paid for entirely by the state. Adopting a similar (national) program spreads these administrative costs across many states, users. Also, adopting a national program is not restrictive since the basic structure can be adopted and then amended as necessary to achieve state-specific goals. Also, outputs from several of these programs can be sent to common programs like Microsoft Word or Excel. Again, the major contenders for this option are:

##### REM/Rate

**Pros**:

-   Excellent support from developer

-   Already approved for Tax Credit certification

-   Used by the majority of energy raters nationally

-   Can be modified for our 2006 IECC reference quickly and cheaply

-   Two layers of input detail.

-   Editable materials libraries

**Cons**:

-   May be weather file issues

-   Uses the new Zero points – Zero Energy Use scale

-   Greater initial training requirement.

**Cost**: See chart

**Timeframe**: 3 months

**Comment**: Clearly the winner among all the responding energy raters/providers

#####TREAT 4.0 (available Spring 2008)

**Pros**:

-   Excellent support from developer

-   Allows user developed report formats

-   Will allow building of weather and material libraries

-   We can create our own reference house sets

-   Will be able to do either indexed or non-indexed point/star ratings

**Cons**:

-   Not yet approved for tax credit certification by RESNET

-   Greater initial training requirement.

-   Not used for ratings in the past – only weatherization

**Cost**: See chart

**Timeframe**: 9 months until release.

**Comment**: Need to reserve judgment until 4.0 is available.

##### Energy Gauge

**Pros**:

-   Already approved for Tax Credit certification

-   Can probably be modified for our 2006 IECC reference quickly and cheaply

-   Broad report spectrum   

**Cons**:

-   Spotty technical support. Questions to the FSEC Executive Director were answered quickly. An e-mail technical support request via their website (their official method) was never answered.

-   Uses the new Zero points – Zero Energy Use scale

-   Greater initial training requirement.

-   Improvement Analysis feature not yet operational

-   Most limited of the three packages from the input flexibility point of view

-   No library view, access, or ability to change

**Cost**: See chart

**Timeframe**: 3 months

**Comment**: Clearly the winner among all the responding energy raters/providers

##### Option D. Multiple platforms

It is conceivable that the best option for ’s situation would be to continue with AKWarm as it exists (with the reference-home library change). RESNET approved programs could be used for situations that require it, such as the federal tax credit program or Energy Star certification.

**Pros**:

-   Only need minor changes to AKWarm which would still be used for AHFC Energy Ratings

-   AKWarm would still be available for free to the public

-   AHFC would not need to train raters to use other software packages

**Cons**:

-   AKWarm quick fix only last as long as Windows XP is predominant

-   Raters still must be certified by RESNET or the equivalent rating network

**Cost**: None to AHFC except library update. Cost to raters would depend on the software they chose to use. AHFC would have no control over that.

**Timeframe**: Depends on how active AHFC is in getting raters approved.

**Comment**: Probably the least cost, fastest way to resolve immediate issues while we continue to contemplate a longer term solution.

##### RESNET Costs

In addition to the costs incurred by obtaining, modifying, supporting, and using the above software packages, there are also costs involved with RESNET certification should AHFC choose to take that path. These include application costs, annual accreditation fees, and rating registration fees. The following is the accreditation fee structure for HERS Providers. The annual fee for accreditation of rating software, and rater training providers is $1750, with a $250 annual discount for entities who are accredited in two categories and a $500 annual discount for entities who are accredited in three categories.

**2005 ENERGY Homes Accreditation Fee**

|**Number of homes**| **Fee** |
|---------------|-----|
| 0 - 500       |$1,750 minimum
| 501 - 1,500   |$1,750 plus $1.75 per rating >500|
| 1,501 - 4,000 |$3,500 plus $1.50 per rating >1500|
| 4,001 - 7,500 |$7,250 plus $1.00 per rating >4000|
| 7,501 - up    |$10,750 plus $0.50 per rating >7,500 up to a maximum of $12,500|

The annual RESNET cost to AHFC if AKWarm was approved as a rating software package would be over $5,500 if we did about 1,000 ratings per year. If we used another accredited program the cost would be $1,750 less.

**Cost Comparison**

|             | **REM/Rate**|**EnergyGauge**|**TREAT**|                                                                                                                                                                                                                                     
|-------------|-------------|---------------|---------|
| **Software Cost and Use Fees** | *Licensed annually to HERS Providers*: Annual Software License Fee - $500                                                                                                                                                                                                        Rating/Use Fee - Applies to each home (unique mailing address) receiving an Energy Rating, Energy Star Home                                                        Certification, or Tax Credit Certification using information generated by the Software.  First 1,000 ratings completed during single contract year: $6 each.  Ratings 1,001 through 2,000 in single contract year:$5 each.  Ratings 2,001 through 3,000 in single contract year:  $4 each.  Ratings 3,001 through 4,000 in single contract year: $3 each.  All ratings in excess of 4,000 in single contract year:  $2 each. | ResRatePro (certified Rater) $149, HERS (Certified) Provider Version $249, Registration per Rating: $20 (Includes QA, database storage of all registered Ratings, Energy Tax Credit Certification Reports and quarterly Ratings Report to Certified Rater, Accredited Rating Providers acting as software distributor or government funded project manager.) If this support is not desired the fee is $5 per rating for up to 200 ratings per quarter.Updates are free for 12 months from the date of purchase. Prices for upgrades are prorated.| Single family version: $495, Multifamily version: $1495, Multifamily version (non-profit / government discount rate): $995.  Each license comes with 12 months of technical support and software upgrades. Each license may be installed on two separate computer.  [*Read software license and support terms*](http://treatsoftware.com/treat_installation_and_support.html)  |
| **Capital Costs** | About $5000 to modify the IECC 2006 reference house with the amendments | Unknown for IECC updates. Must use TMY weather data that is already in place. Can’t update weather files or other libraries.| Providers can build their own reference houses and develop our own weather tables|
| **Support**       | $100/hr consulting| On-line knowledge-base and user forum|Single Family Version: $200 annually,  Multifamily Version: $400 annually |
| **Training**      | Probably need to send trainers | Web-based or we can send staff to to become trainers.| Interactive webinar.|
| **HERS Certified?** | Yes | Yes| No. But is in submission process.|
| **Tax-Credit Certified** | Yes | Yes | No |
| **Engine**   | Internal correlation| FSEC-enhanced version of DOE-2.1E | SUNREL (From NREL)|
| **OS**       | Windows only | Windows only (okay) | Windows only|
| **Reports**  | Air Leakage, Component Loads Summary, Component Consumption Summary, Component Design Loads Summary, Economic Summary, Emissions Report, Energy Cost and Feature Report, Equipment Sizing, Fuel Summary Report, Lights and Appliances, Performance Summary, Performance Factors, Source Energy & Emissions Report, 2005 EPAct Tax Credit The home must be inspected/approved by a certified HERS rater to receive credit, Utility Bill Reconciliation, ASHRAE 90.2 Reports, Energy Star Reports, IECC Compliance Reports, MEC Compliance Reports, Energy Appraisal Addendum, Energy Loan Application, Home Energy Rating Certificate, LEED for Homes Checklist, Satisfactory Completion Certificate , Summary of Reports Selected, Error Report, Improvement Analysis Report | Annual Energy Summary, Comparison Reports, Disclosure, DOE-2 Reports, Fannie Mae, HERS Summary, Improvement Package, Input Summary, Monthly Summary, Photovoltaics Summary, Pollution Analysis, Specific Hourly Report Inputs, Worst Case Summary, Reference Home Characteristics, Tax Credit The home must be inspected/approved by a certified HERS rater to receive credit. | The Fuel Bill Release report, Building Description, The Design Heating and Cooling Load Model Energy Report, Base Load Report, Occupant Lifestyle Savings report, Model to Actual Comparison of Base Usage table, Visual Inspection and Measurements reports, Improvement Packages report, Workscopes report, Normalized Model to Billing Comparison report, Investment Guidelines for Heating Heating Energy Scorecard, Normalized Annual Billing Savings Tracking report, Actual Billing to Model Comparison report, Customer Information and Mail Merge report, Data Collection Forms|
| **Other features**| User Defined Reference Home feature enables the HERS provider to create other reference homes (local construction practice, local code) that can be compared to the rated home.  Export Database feature creates a database of inputs and outputs for statistical analysis, archiving ratings and custom report generation.  **Batch Mode**: allows you to create a list of buildings (batch) to run all at one time to make changes or for comparisons | Ideal for evaluation of low energy and Zero Energy Building Designs.  Hourly prediction of solar electric PV system performance.  Hourly prediction of solar hot water heating systems. Hourly prediction of end-use electrical and gas energy consumption for evaluation of peak impacts. | Input of visual inspections, Lifestyle impact analysis, Combustion Air Calculator, Utility Bill Importer, The Daily Weather Data Import utility, The Model Inspector utility, Can model building as single space or multiple spaces |
| **Libraries**   | User defined and program defined (locked) building component, improvement options, utility costs | Program defined only – no access | **Editable libraries**: User, Customer, Contractor, Daily Weather Data and Fuel Rate. **Non-editable libraries** including the Fuel, Surface, Door, Glazing, Window Frame, Lighting, Appliance, Heating, Cooling and Domestic Hot Water |
| **Files**     | RemRate saves each building as a quantifiable file that can also be entered into a database | EnergyGauge stores all of the building data in a database and allows you to save the building as a discrete file (.enb) | TREAT projects are created and stored in Treat Project Group (TPG) data files. Each TPG may contain one or more projects created by the user. Each TPG is stored in a single file with a TPG extension. *Support for multiple Project Groups:* each project group represents a single TREAT database. *Archiving and data-compression:* a TPG file is a compressed TREAT database. It reduces the disk space needed to store the TREAT database by 50% -90%.|
| **Climate** | winter design temp as -6 F | Anchorage Winter design temp -18F | Anchorage Winter design temp -18F|
