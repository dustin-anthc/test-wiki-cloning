- [Overview](#overview)
- [Define the prototype home for each region](#define)
- [Model the prototype homes in AkWarm using most recent BEES prescriptive values](#model)
- [Determine Final BEES Rating](#determine)
- [Results](#results)

# Methodology for Updating AKWarm to Current Alaska Building Energy Efficiency Standards

<a name="overview"></a>
## I.  Overview

        The Alaska Building Energy Efficiency Standards (BEES) are created by modifying the International Energy Conservation Codes (IECC) to fit Alaska’s unique climate and construction conditions.  The BEES then are presented to Alaska Housing Finance Corporation (AHFC) board for consideration, public hearings are held, and finally a version of BEES is adopted.  For homes to be financed by AHFC, they must meet the Alaska BEES which can be met by either the prescriptive or performance path.  The prescriptive path requires that each building component is shown to meet the individual requirement within the BEES standard. For energy efficiency certification, the performance path requires modeling the whole building using AHFC’s AKWarm software and scoring at least 83 points on the AKWarm rating scale (otherwise known as Four Star Plus).

           Every three years IECC is updated (most recently 2012) and as a result, BEES should be updated every three years.  This means that the rating required to meet BEES, as calculated in the AKWarm software, must be recalculated every three years, and regulations must be reviewed, and perhaps changed.  The Cold Climate Housing Research Center (CCHRC), in partnership with AHFC and Analysis North, has developed a modeling methodology to update the AKWarm rating score required to meet 2009 and future BEES updates.

        In order to minimize the changes that people who use the AKWarm software will face, AHFC decided to update the AKWarm rating needed to meet BEES, rather than updating the reference house and thereby disrupting the point scale Alaskans are used to.<span id="ftnt_ref1" class="anchor"></span><sup>[1]</sup>  Thus, to preserve the knowledge of homeowners, builders, and raters, CCHRC created prototype homes using regional averages of building characteristics obtained from the Alaska Retrofit Information System (ARIS).  These prototype homes were then modeled in AKWarm using the new BEES (2012) prescriptive values, and the rating points calculated for each.  By taking the average rating for all of the regional prototypes combined, a new rating point value required to meet the 2012 BEES requirements was determined.  

        We recommend that this modeling process be undertaken each time BEES is updated to reflect the new IECC standards.  In order to facilitate this, a detailed description of the modeling methodology follows.  

<a name="define"></a>
## II.  Define the Prototype Home for each region
  Use ARIS data for homes rated within the past six years that meet the last update of BEES to create an “average” home for each region

1.  **Query ARIS for appropriate data**:  Download data for all BEES and As-Is records into Excel.  The As-Is files were included because many recently uploaded BEES files were incorrectly classified as “As-Is.”  BEES files accounted for 94% of the data used for these prototype homes, with the As-Is files with an AKWarm rating of 83 or above accounting for the rest.  

**Required Fields -** Each file contained the following fields:

1.  LocationID

2.  HouseType (Single family, multi-family, etc.)

3.  City

4.  RatingPoints

5.  RatingType

6.  YearBuilt

7.  Volume

8.  floorsqft

9.  GarageSize

10. GarageArea

**Component Fields -** As each home component is entered in ARIS as a separate record, each component type (windows, floors, etc.) was downloaded as a separate file.  In addition to the required fields above, the following additional fields were included:

1.  CompType (component type)

2.  idname (rater entered component name)

3.  Size2 (calculated size)

4.  GrossArea

5.  Additional component fields, as needed (Orientation for windows, GradeDistance for below grade walls, etc.)

<!-- -->

1.  **Filter Excel Files:**  Using the filters in Excel, the files were trimmed to include only the specific year, type, and region needed.

<!-- -->

1.  Filter →  BEES and AS-IS only

2.  Filter → Ratings \> or = 83

3.  Filter → Year Built \> or = 2006.  Note:  the Arctic region had to use files from homes built since the year 2000 because the initial query only returned 2 single family home records.  

4.  Filter → Single Family homes only.  

5.  Filter → Cities in 1 of 5 regions.  Note: The cities’ regions were determined using the five regions defined in the State of Alaska Energy Conservation Standard for New Residential Buildings (1988)

6.  For components that needed to be separated into garage and non-garage data, a filter was used based on the **IDName** field to split the data into separate Excel sheets.

<!-- -->

1.  **Find Component Averages:**  For each region, the average component values were determined using the following procedure:

<!-- -->

1.  **Count** the number of unique ratings using the **LocationID** field in Excel

2.  **Sum** the area of the component for all records (there will often be more than one record for each unique home)

3.  **Divide** this sum by the number of unique ratings

        

        

1.  **Determine Foundation Type:** After dividing the floor components into **garage** and **non-garage** data, the **component type ID** field and the **distance below grade** were used to determine whether foundations were above grade, on grade, or below grade by the following procedure:  

<!-- -->

1.  Calculate the **total area** for **each foundation type**

2.  Assign each region a **home foundation type** and a **garage foundation type** based on whichever one had the **greatest total area.** 

3.  Weight the below grade walls and floor areas to account for the range of foundation types. <span id="cmnt_ref1" class="anchor"></span><sup>[a]</sup> 

<a name="model"></a>
## III.  Model the prototype homes in AkWarm using most recent BEES prescriptive values

**1.  Create an AkWarm file for each prototype home**: Using the averages obtained in part II, create a separate AkWarm file for each region.

**2.  Input BEES Prescriptive Values:**  R-values and characteristics of the components in the AkWarm files were assigned primarily using **Table A402.1.1** in the residential energy efficiency section of the most recent version of BEES.  As not all the prescriptive values translate directly into exact components, the following assumptions were made:

-   If wall R-values were greater than 21, XPS exterior sheathing (R5 / inch) was added in the size increments required to reach the prescribed value

-   Energy truss roofs with the lower ceiling R-value were used

-   Both windows **and** doors use fenestration values

The details of inputs were recorded in an Excel spreadsheet; for 2009 and 2012 BEES please refer to the tables below for a more in-depth description of the prescriptive values used in the prototype homes.  

**3.  Determine space / water heating systems:**  The Department of Energy federal minimum guidelines were used to determine the space and water heating systems used in the prototype homes.  Because the South-central region’s primary heating fuel is natural gas, it was modeled using a natural gas boiler system.  All other regions primarily use \#1 fuel oil, so they were  modeled with boilers using \#1 fuel oil.  AKWarm uses a space heating AFUE of 80% and a water heating Energy Factor of 0.6 for all regions, which are also used in this model.<span id="cmnt_ref2" class="anchor"></span><sup>[b]</sup>

<a name="determine"></a>
## IV.  Determine Final BEES Rating

**1.  Calculate rating for each region:**  Once all of the components and prescriptive values were entered into AKWarm for each region, the ratings were calculated automatically.

**2.  Determine rating needed to meet BEES:**  The average rating for all five regions was calculated, and if it was within one point of an AKWarm star level, it was rounded to that value, otherwise it was rounded to the nearest whole point.

 
<a name="results"></a>
## V.  Results 

**2009 BEES:** Using the 2009 BEES prescriptive values, the average rating was 83.62, which would be rounded to 83, as that is the lower boundary for a 4-star plus home and the present AHFC star rating required to meet BEES.  Upgrading to BEES 2009 from the original AKWarm BEES values did not produce significant change in respective point ratings largely because the reference houses originally programmed into AKWarm had much lower ACH<sub>50</sub> values.<span id="ftnt_ref3" class="anchor"></span><sup>[3]</sup> The 2009 BEES requirement was an ACH<sub>50</sub> equal to seven or less.  This compares to AkWarm’s model homes that have an ACH<sub>50</sub> of four for the Southeast, South-central, Interior and Northwest regions and three for the Arctic region.  

**2012 BEES:** Using the anticipated 2012 BEES prescriptive values, the average rating was 89.52, which would be rounded to 90, since it is not within one point of a star boundary.  Based on these results, a home following the performance path needs to receive an AKWarm score of 90 or above to meet the anticipated 2012 BEES, which falls within the Five Star range.  BEES 2012 required an ACH<sub>50</sub> of three, which is equivalent to the previous requirements for the Arctic region and more stringent than the the previous requirement for the Southeast, South-central, Interior and Northwest regions.

[1] For example, a building scoring 88 points before the reference house change may only obtain a rating score of 83 points after the update process.  This could cause potential confusion among homeowners who have purchased a home marketed at a certain star level, builders who have learned how to produce a home meeting a certain star level, and energy raters who make recommendations based on the cost of an improvement versus the number of points gained towards a Home Energy Rebate.

[3] ACH<sub>50\\  </sub>is equal to the number of air changes per hour in a building, induced by a 50 Pascal pressure from blower door operation.

[a]dustin:

Change to % floor type for each foundation type, as per conversation with Alan on 8/30/2012

[b]dustin:

Change to Federal Minimums (after modeling) as per conversation with Alan on 8/30/2012
