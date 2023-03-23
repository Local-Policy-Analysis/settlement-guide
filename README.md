# Calculating CSP

Here I have tried to explain how we calculated CSP in 2022 for the 2023-24 settlement (we'll hopefully add in other Settlement products later)

Good luck with the Settlement.

## What is a Settlement, what's a CSP and what have I got myself in for?

There is a page of definitions [here](/glossary.md), but as a quick intro: 

The Settlement sets out how much money central government will pay Local Authorities through grants each year. (This is not in fact all of the money that central government pays to local government, but as you have probably gathered, local government finance is very complicated). **C**ore **S**pending **P**ower is a constucted measure of comparing Local Authorities essentially. We add up all of their grants from the Settlement, and the Council Tax they raise, and imagine that this is the amount of money they have to spend. While this clearly isn't actually true, (we're missing a lot of money that goes to them through other means, as well as not taking into account their current financial position), it provides a useful comparison point for LAs year-on-year. As soon as you publish this, the Local Government Association will publish an article with their view on the percentage increase in CSP for example.

Inside CSP we also calculate a lot of the grants that go to local authorities (for more details, see the glossary), and Section 151 Officers will use it to calculate their budgets for next year. We actually calculate the Settlement twice: Provision Settlement in December is theoretically a consultation document, where authorities can disagree with the methods or calculations, and then Final Settlement, which is usually materially the same early in the new year.

### What am I actually making?

You will make a lot of final products, but most of them are single columns of numbers for individual grants. The two all-encompassing products are the `Core Spending Power Summary` and `Core Spending Power Supporting Information`. You need to calculate everything in these except the SFA. (If you look at the number of columns in the Supporting Information table, you will see why these instructions are so long). Most of them are quite simple though.


## Required Files

| File | Location | Purpose |
|------|----------|---------|
|Authorities and their corresponding Precepts | [gov.uk](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/966850/Final_LCTS_grant_allocations_2021-22.xlsx) (**Note**: This is for 2021 Authorities. If you can find a better one, you should use that instead. You would think that there was a standardised list somewhere, but you would be wrong. You will also notice that this is fact just a random grant determination letter that happens to have the information we want in its output. You need to take what you can get. Make sure to get someone to confirm your precepts list.) | Needed to calculate tax bases for precepting authorities |
|Table 9 (Current Year) | [gov.uk](https://www.gov.uk/government/collections/council-tax-statistics) | Current Council Tax Base and Average Band D |
|Table 9 (Current Year - 4) | [gov.uk](https://www.gov.uk/government/collections/council-tax-statistics) | Historical Council Tax Base to calculate projections |
|List of restructured authorities with ONS codes and Ecodes | If there were no restructures in the previous year, take from last year's settlement. If there were, ask whoever is running the settlement for an updated copy | Allows you to restructure historical data to match current LAs |
| CSP Supporting Information Table | [gov.uk](https://www.gov.uk/government/publications/core-spending-power-final-local-government-finance-settlement-2022-to-2023) (Note, you want the most recent LGFS, but there isn't a collection page, so you may have to google. You want to import the hidden tab called `inputs`.) | Any grants whose values are being rolled over. Most of the information in this table will also go into your Supporting Information table as well, so you will need to copy it across. |
| SFA, BFL and RSG | You will get this as an input from the SFA team | SFA is just a column in CSP. BFL is used to calculate underindexing. You might use RSG to calculate any floor/funding guarantee. It's also a useful output for whomever is writing the Key Information Tables |
| Last Year's RSG | I'm not sure. I asked the SFA team. Hopefully someone in the future will update this to know. | Used to calculate the floor grant/funding guarantee if it exists.
| RNF | Ask the funding reform team for their most up-to-date list. | Several grants (notably those related to ASC) are given out proportionally based on the RNF |
|Number of Dwellings | [gov.uk](https://www.gov.uk/government/collections/council-taxbase-statistics) You want `Council Taxbase: Local authority level data` for your year| This is used to calculate Area CSP, and to calculate CSP per Dwelling for the CSP summary |
| New Homes Bonus | This should be given to you by whomever is running Settlement | It's a column in CSP. Also possibly used in any floor/funding guarantee calculations 

### Points to Note

Sadly, government spreadsheets are very rarely perfect rectangles with no errors, and so there are some exciting traps to note when importing the data

<details>
    <summary>Current Table 9</summary>
The `Data` sheet of Table 9 contains the Average Band D and Council Tax Base, for both billing and precepting authorities that we need to calculate the Band D and CT Base for next year. However, the two table are directly above each other and **the columns of the billing and precepting authorities do not line up**. 

For Billing Authorities, Council Tax Base is in the column **7. Council tax base for council tax setting purposes** Band D is in the column **9. Average (Band D 2 Adult equivalent) council tax (including Adult Social Care precept and excluding local precepts)** corresponding to the year. However, when an LA has been restructured but their Ecode hasn't changed, some information for that authoritiy is written in another table to the right of the main data table. In 2022-23 for example, the Band D figures for West Northamptonshire and West Suffolk are given in column 82. This may be fixed in the future, but it is worth checking that each billing authority has a Band D and a Tax Base when importing. Similarly, this table does have ONS codes in it, but they are to the far right of the table, in the final column.

For Precepting Authorities, Band D is in the column **3. Average (Band D 2 Adult equivalent) council tax of major precepting authority (line 1 / line 2)** (Note that this is not the column directly underneath the billing authority band Ds). The Council Tax Bases of the precepting authorities are not calculated the same way that we require them, and so you will need to **sum the tax bases of the corresponding billing authorities, and not import these from the spreadsheet**. (For example if Precepting Authority Madeupshire is formed of Bigtown and Ruralington, the CTB of Madeupshire should be the sum of the CTBs of Bigtown and Ruralington). If you do not do this, everything will not add up correctly at the end. 

You will not need the rows for Police Authorities, or Combined Authorities, however you need to make sure to keep the rows for E5101 (Whole of GLA's Area) and E5102 (London Boroughs Less CoL) because they have complicated council tax. You also need to keep Greater Manchester Combined Authority. You should treat this as a fire authority, and assign it the Band D value that will hopefully be given to you by whoever is running the Settlement

> **Note on GLA** - The GLA tax base is troublesome. You will need the total tax base for All London Boroughs including CoL (E5101), and All London Boroughs minus CoL (E5101). Just for clarity because I struggled with this idea, the CT Base for E5102, is `CT Base for E5101 - CT Base for E5010` (E5010 is CoL) This is not included in the precepts input, and you will need to calculate it manually. 

</details>

<details>
    <summary>Past Table 9</summary>
All of the points for Current Table 9 apply to Past Table 9, however we also need to restructure the Table 9 from the past, so that it has the same LAs as now. We only care about the Council Tax Base from the past though, and we only want it for the billing authorities. Don't do extra work you don't need to, as you would just discard them again later

##### Restructuring

This has the potential to be terrible, but luckily no authorities have been split up, only joined. Remove all upper tier authorities from the list of restructuring authorities, and add the lower tier tax bases of the restructured authorities together to get the equivalent tax bases for the new authorities. E.g.:


| LA Name      | Class | New Code | Whole or part of previous authority | ct_base_past |
|--------------|-------|----------|-------------------------------------|--------------|
| Xmouthshire  | SD    | E111     | Whole                               | 20           |
| Yborough     | SD    | E111     | Whole                               | 15           |
| Overallshire | SC    | E111     | Part                                | 100          |

should become

| LA Name   | Class | New Code | ct_base_past |
|-----------|-------|----------|--------------|
| Newington | UA    | E111     | 30            |


Ignore all precepting authorities (e.g. fire services), as they will be recalculated each year anyway.

For information on 2023-24 restructures specifically, see [2023-24 restructures](/Readme/2023-24-restructures.md)
</details>

<details>
    <summary>RNF</summary>
Not every authority will have an RNF. That's okay. Just check that the recently restructures authorities do that them. A good quick check at this point is that your RNF still adds up to 1.
</details>

<details>
    <summary>Last Year's CSP Supporting information Table</summary>
You do not need every column from last year's CSP table to calculate this year's CSP (you only really need the CSPs from previous years, any grants you are rolling forward, and the NHB, however you will need to output them all into the CSP summary Table for this year anyway it's easiest to import everything at the start). **Note:** Several of these columns are likely to have similar names to things you want to name columns, so be careful.
</details>

<details>
    <summary>Last year's RSG/SFA information</summary>
You will need this to calculate any funding guarantee or floor grant at the end. There are no surprises though, although you will not end up needing all of the columns. It's worth adding a prefix to the coumn names here too so that they don't clash.
</details>

<details>
    <summary>This year's SFA</summary>
If this is difficult to import, you need to tell the SFA team to fix their input.
</details>

<details>
    <summary>New Homes Bonus</summary>
You want `Year X Payments (£): inc. empty homes.` (unless they've changed the spreadsheet)
</details>

<details>
    <summary>Dwellings</summary>
    Similarly to Table 9, this sheet is full of traps. You should discard the figures for precepting authorities, and sum the dwellings in each correcponding billing authority to find the number in the precept.
</details>

## Council Tax

We want to calculate the "maximum" council tax that LAs will theoretically be able to collect during the year (i.e. if they increase their council tax by the maximum they can without triggering a referendum). To make life easier, we also assume that everyone will pay band D. We thus need `band_d` and `ct_base` for the relevant year.

### Band D

We apply the referendum principles to the current band Ds, in order to get the new Band D value. 

Generally referendum principles are in the form (maximum of 3% and £5), so an authority whose Band D was £200 would increase their Band D to £206 (a 3% increase), but one whose Band D was £150 would increase it to $155 (because £5 is more than the 3% increase of £4.5). Not all types of authorities have this form (e.g. core authorities don't have a potential cash increase because it would always be smaller than the percentage increase) but they can all be treated this way.

In general, we take takes the `Average (Band D 2 Adult Equivalent) council tax (including ASC precept and excluding local precepts)` from **Table 9** for non precepts, and ` Average (Band D 2 Adult equivalent) council tax (including Adult Social Care precept and local precepts)` (for precepts), and calculate
`max(previous * 1.x, previous + y)`, where `x` is the maximum percentage increase and `y` is the flat cash increase.    

This is complicated as authorities with an Adult Social Care responsibility get an extra increase. This extra percentage increase occurs at the same time as the base increase, so for example an authority might get a 3% increase for being a core authority, and a 2% increase for being an ASC authority. Their Band D would therefore increase by 5% (you will sometimes hear people talking about something like a 3+2% increase. This is what they mean). **It is NOT a 3% increase and then a 2% increase**

So an authority with a £200 previous Band D and a 2+3% increase should end up with a new band D value of £210.

Once you have calculated the new value, round it down to the nearest penny.

You will need the amount raised by the ASC precept increase later, so it can be worth keeping this separate (although see the warning below)

> **Warning** This sounds easy, but R is not good at rounding numbers and does not to my knowledge have a good way of fixing the problem. Try doing `floor(141.42*100)/100 ` to discover the joy. If you do not all use the same method for solving rounding, you will all get different numbers. You will also get different numbers if say you calculate by doing `previous * 1.03`, and your double-runner does `previous + previous * 0.03`. This can be worth doing to check if you have made a mistake, as you will still get similar numbers, but you should decide on a unified approach for the final figures. In another branch I have fixed this using Reticulate and Python's `Decimal` class)

For clarity

| Authority Type | Authority Classes |
|----------------|-------------------|
| ASC Authorities| London Boroughs, Unitary Authorities, Metropolitan Districsts, Shire Counties |
| Core           |London Boroughs, Unitary Authorities, Metropolitan Districts|
| Districts      |Shire Districts |
| Fire           | Fire Authoritiesl, Combined Fire Authorities |
| Police         | Police (which we don't calculate), GLA minus CoL (E5102) | 

### Council Tax Base

Precepting Authorities do not collect council tax themselves. They are larger, overarching authorities, and their CT base is the sum of all of the billing authorities that make them up. Thus, to calculate the CT base:

1. Remove all precepting authorities

1. For each remaining LA, calculate:

$$g = \left( \frac{\text{Taxbase(curr-year)}}{\text{Taxbase (curr-year - 4)}}\right)^\frac{1}{4}$$

$$\text{Taxbase(next-year)} = g \cdot \text{Taxbase(curr-year)}$$

Then for each precepting authority, sum their constituent authorities (from `LCTS Lookup.xlsx`) to find their tax base. 

However! There is at least one precepting authority who is not included in the spreadsheet, so we need to fix them:

 - GLA - The "whole GLA" is made up of all London Boroughs. Their band D tax rate has been split up into two parts, the police district, applied to 
    everyone except the City of London, and a core part, which applies to everyone. Thus we need to know the tax base for everyone except CoL
    (for the former part), and everyone in London, (for the latter part). GLA's total tax requirement will be both added together.

### Council Tax Estimations and Projections

We need values for both the Council Tax estimates for the current year *and* next year. This is because the values for the council tax base you have read in are more accurate than the projection used last year, and LAs will want to be able to compare to this more accurate figure. (As a warning, Council Tax for the current year is one of the things that you imported from last year's CSP summary table. It's probably best not to overrite your import, as you might need it, but it's also important to keep track of which value is current, and which was imported. Good luck.)

For the current year

$\text{ct-current} = \text{Taxbase(curr-year)} \cdot \text{Band D(curr-year)}$$

And for next year

$$\text{ct-next} = \text{Taxbase(next-year)} \cdot \text{Band D(next-year)}$$

## Underindexing

They keep threatening to get rid of underindexing, so first check it still exists. Then go and ask the Business Rates team what the multiplier is. It's probably the change in RPI for the preceeding year (e.g. if you're calculating the 2024-25 Settlement, it's probably $$\frac{\text{RPI for 2023}}{\text{RPI for 2022}}$$), but it varies a little. The multiplier is the same for all LAs. 

$$\text{under-index}_i = BFL_i * \text{Underindex-multiplier}$$

## Uprated Grants

<details>
<summary>What is Uprating?</summary>
Uprating is a fancy term for taking last year's numbers for the grants, and then multiplying them by a number.

You may ask: "What about all of the decision that went into those numbers. Don't we need to re-evaluate them to make sure that they're still relevant to all of the authorities?", and someone will answer "That sounds like an exellent idea. You can do it. Also make sure you find someone else to double-run your answers. You'll also need to clear your new distribution with policy. 
Hence: uprating. 

Rolling over grants is just uprating but we multiply the grant by 1 (i.e. it's still the same). Not to be confused with rolling *in* grants.
</details>

As a brief warning, anything that says "grant" is subject to be randomly changed by policy while you're working on it. Don't try and build something complicated that does multiple grants at once, because you'll just have to dismantle it because they've decided that those grants should actually work differently at the last minute. 

This is also likely to change, but a number of grants are just uprated. In 2023-24 these were:

- Rural Services Delivery Grant (RSDG)
- improved Better Care Fund (iBCF)

In 2023 each LA recieved the same as in 2023, however they could also be increased by a multiplier (or something else fun might happen!)

## Other Simple Grants

### ASC Market Sustainability and Improvement Fund

This grant keeps changing its name, so who knows what it'll be called. It used to be called "Fair Cost of Funding". Aside from its confusing policy implications it's easy to distribute though, and is also just the RNF. 

For fun times, there's a grant with a very similar name to this (Market Sustainability and Fair Cost of Care Fund), which was distributed in 2022-23. Don't mix them up.

### ASC Discharge

This is distributed with the same shares as the iBCF, however it's a separate grant.

## Social Care Grant

This grant was a bit weird for 2023. Most of it will probably just be uprated in the future if it doesn't get reformed. 

The theory is that SCG plus the money that LAs collected through their ASC precept increases should be distributed approximately through RNF. This isn't actually happening though, so we take some money as an [equalisation grant](#equalisation-grant) to try an even it out.

For 2023-24 we added some new money, which was distributed according to the RNF, then added to the previous year's SCG funding. This total forms the basis for SCG. We use some extra money for the equalisation grant.

### Equalisation Grant

1. Calculate the amount raised by each LA by the increase in their Band D by the ASC referendum principle. 
    E.g. if ASC precepts increased by an extra 2%, you would do  $$0.02 \cdot \text{Band D(current-year)} \cdot \text{Taxbase(next-year)}$$

    It is also possible you worked this out as part of calculating the [council tax totals](#council-tax-estimations-and-projections) and so you can use that figure. For each LA $i$, call this figure $\text{ct-ASC}_i$
1. Sum this to find the total amount collected by the ASC increase. Add the total available for equalisation. We will call this $\text{ASC-tot}$.
1. Distribute $\text{ASC-tot}$ according to the RNF. For each LA $i$, call their share $\text{ASC-tot}_i$. Ideally, this would be how the funding was distributed, however some LAs will now get less than they raised via Council Tax, which is not allowed. 
1. For each LA, calculate 

    $$eq_i = \max (0, \text{ASC-tot}_i - \text{ct-ASC}_i )$$

    This gives all LAs either 0, if they already gain more than their share in CT, or what would equalise their share if not.
1. However we have now distributed too much grant, as several of the authorities would have got negative amounts under the original distribution, and so we need to scale all of the amounts by 

$$ \frac{\text{Total available for equalisation}}{\Sigma_i eq_i}$$

Adding these scaled values to the SCG basis we calculated above gives the SCG.

## Current Year's CSP

You need to recalculate the CSP for the current year using your new figure for council tax. If there has been no restructuring, or rolling in grants, you should be able to do this by subtracting the CT given in the previous CSP supporting information from last year's CSP, the adding $\text{ct-current}$ from [above](#council-tax-estimations-and-projections). If there have been restructures, be careful with this.

## Servces Grant

This is highly likely to be changed in the future, but for the 2023 Settlement:

The total sum allocated to services grant is divided between two grants, Services Grant itself, and the funding guarantee. For the allocation itself, see [funding guarantee](#funding-guarantee).

The total amount for Services Grant is calculated by:

 - 822 mn (previous year's grant)
 - (-30) mn Family Support
 - (-27.1) mn BR Relief
 - (-80) mn [Equalisation](#asc-equalisation)
 - (-30) mn Contingency
 - (-188) mn NICS
 - (+111) mn LTSG
 - (-RSG 2023)
 - (+ RSG 2022)
 - (-NHB 2022)
 - (+ NHB 2023)

i.e 577.9 mn - increase in RSG since last year + decrease in NHB since last year

This sounds easy, however because of pilot grants (which I do not understand, so someone else will need to write an explainer on that), calculating the change in RSG is harder than it looks. I *think* you need RSG including 50% pilots, but you should ask the person running the settlement if this is still happening for some reason. Anyway, both RSGs need to be the same type. I couldn't get the numbers, and so as RSG is just inflated each year, if you have the sum of RSG for one year, you can caluculate the previous/next year by multplying or dividing by the inflation factor. 

$$\text{RSG Inflation Factor}_i = \frac{\text{CPI(September-current-year)}}{\text{CPI(September-previous-year)}}$$

Remember that you don't need to calculate the RSG and NHB differences for each LA, just overall.

Isle of Wight then get £1m from a left-over grant.

### Funding Guarantee

*According to policy, this will definitely not exist next year. Some kind of floor grant might though.*

The idea of the funding guarantee is that every LA will have at least a 3% increase in Constructed Core Spending Power (ignoring rolled in grants). Confusingly, this is not quite the same as normal CSP. 

<details>
<summary>What is Constructed CSP</summary>
Define $\text{constructed-ct(2023)}$ as 

$$\text{constructed-ct(2023)} = \text{Band D(2022)} \cdot \text{Taxbase(2022)}$$

then

$$\text{constructed-csp(2023)} = (\text{csp(2023)} - \text{ct-total(2023)}) + \text{constructed-ct(2023)} - \text{rolled-in-grants(2023)} - \text{ilf(2022)}$$

(Essentially, it's CSP but with last year's band D and no rolled in grants)

</details>

The idea therefore is that we take some part of services grant and distribute it among the LAs as a *funding guarantee grant*. We then distribute the remaining services grant using the same proportions as last year. We want to give out the minimal amount of guarantee such that giving out the remaining grant causes each LA to have a $\text{constructed-csp}$ at least 3% higher than their 2022 CSP.

> **Warning** This 2022 CSP is also a trap. This is the 2022 CSP that was calculated back in [current year's csp](#current-years-csp), i.e. the 2022 CSP calculated with updated CT base numbers. However for 2022 there is also a figure calculated with grants rolled in (see notes for 2022-23 rolled-in-grants). We don't want that one.

I recommend trying to solve this problem yourself. It's by far the most entertaining bit of the entire settlement. 

<details>
<summary>Just tell me how to calculate it</summary>

For LA $i$, define their 2023 CSP  as

$$\text{csp(2023)} = A_i + s_i(Y-\sum\limits_{i} x_i) + x_i$$

where 

$$A_i = \text{sfa(2023)}_i + \text{underindexation(2023)}_i + \text{ibcf(2023)}_i + \text{scg(2023)}_i + \text{nhb(2023)}_i + \text{rsdg(2023)}_i + \text{asc-sustainability(2023)}_i + \text{asc-discharge(2023)}_i + \text{ct(2023)}_i + \text{ilf(2022)} + \text{1 mn if IoW}$$

(i.e. $A_i$ is CSP 2023 without services grant or rolled in grants)

$s_i = \text{share of Services Grant (as a decimal)}$

$Y = \text{total services grant funding}$ (not including the 1mn for IoW)

$x_i = \text{funding guarantee}$

Then we can define $\text{constructed-csp(2023)}$ as

$$\text{constructed-csp(2023)} = s_i(Y-\sum\limits_{i} x_i) + x_i + A_i + B_i$$

where 

$$B_i = \text{Band D(2022)} \cdot \text{Taxbase(2023)} - \text{rolled-in-grants(2023)} - \text{ilf(2022)} - \text{ct(2023)}$$

(Notice that $ct(2023)$ and $ilf(2022)$ are added in A and subtracted in B. This can in fact be skipped and is included for clarity.)

We want to find values of $x_i$ such that

$$\text{constructed-csp(2023)}_i - \text{csp(2022)}_i \cdot 1.03 \geq 0$$

i.e. $$s_i(Y-\sum\limits_{i}x_i) + x_i + C_i \geq 0$$

where 

$$C_i = A_i + B_i - 1.03 \cdot \text{csp(2022)}$$

We therefore want to find $min\sum\limits_{i} x_i$, such that

- $x_i + s_i(Y-\sum\limits_{i}) + C_i \geq 0 \forall i$
- $x_i \geq 0 \forall i$

This is a linear programming problem, and can be solved a number of ways. You can use the simplex algorithm, or the r packages `optim` or `lpSolve`.

The funding guarantee for LA $i$ is thus the $x_i$s which satisfy the restrictions, while the remaining services grants is $s_i(Y-\sum\limits_{i})$.

Remember to add £1mn to IoW's services grant (this has been accounted for in the calculation, but isn't included in the services grant allocations yet).

</details>

## CSP

Take all of the grants you've calculated (being careful not to add any twice, I'm looking at you components of Social Care Grant) and the Council Tax projection and add them together to give CSP.

<details>
<summary>Components of 2023-24 CSP</summary>

 - SFA
 - Underindexation
 - Council Tax
 - iBCF
 - Social Care Grant
 - New Homes Bonus 
 - Rural Services Development Grant
 - ASC Market Sustainability Grant
 - ASC Discharge Funding
 - Funding Guarantee
 - Services Grant

</details>

## England Total

The top row of the output spreadsheet is an England Total row, and so you will need to calculate an England Total for all of the grants you have assigned, as well as CSP, CT and the CSP for the previous year. (Or just all of the columns in the output). This is a little bit of a trap as every column is just the sum of its components, except dwellings. Here you should sum only the billing authorities (as the precepting authorities were calculated earlier as the sum of the billing authorities)

# Additional Outputs

## CSP per Dwelling

The CSP summary sheet gives CSP per dwelling for each authority and England overall. Just divide CSP by number of dwellings. You need to do this for both the current year and next year, and both should be divided by the same number of dwellings (it should give a simple comparison for each area).

## CSP Change

You will need to calculate the % change in CSP for both years you've calculated CSP for (so the current year from last year, and next year from this year. Life is much easier if you output this as a decimal)

## Area CSP

This isn't in any of the outputs, but we use this to calculate some statistics for speeches. It tries to take into account the CSP for each billing authority and its corresponding precepting authorities. 

For each billing authority $i$ with precepting authorities $p^j_i$:

$$\text{Area CSP}_i = \text{CSP}_i + \sum\limits_{j} \frac{\text{dwellings}_i}{\text{dwellings}_{p^j_i}}$$

# List of expected outputs

- `e_code`
- `ons_code`
- `ct_total_xxxx` - CT total for current year
- `ct_total_xxx1` - CT total for next year
- `nhb_xxx1` - NHB total for next year
- `under_index_xxx1` - underindex for next year
- `rsdg_xxx1` - rsdg for next year
- `ibcf_xxx1` - ibcf for next year
- `asc_discharge_xxx1` - asc discharge for next year
- `scg_xxx1` - social care grant for next year
- `asc_sustainability_xxx1` - ASC sustainability for next year
- `csp_xxxx` - CSP for current year
- `csp_xxx1` - CSP for next year
- `dwellings_xxxx` - dwellings
- `csp_dwelling_xxxx` - csp per dwelling for current year
- `csp_dwelling_xxx1` - csp per dwelling for next year
- `csp_change_xxxx` - csp percentage change for current year from previous
- `csp_change_xxx1` - csp percentage change for next year from current

If you have all of those, and they double match, you can make the spreadsheets! (Unless someone has changed something, which they probably have.)
