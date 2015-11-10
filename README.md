# Building The Dancing Dog Pricing Structure
# and Product Selection

##  A Classification Problem

This repository contains the documentation of the creation of the financial information for the business plan of The Dancing Dog, a craft beer bar with quick serve food which was to be developed in Seattle, Washington.  

The process of creating the business plan originated with a feasibility study and forecast creation to see if the efforts would be warranted.  As there was no access to wholesale pricing, the business case was built upon webscraped retail data on December 9, 2013.  By webscraping the webpages of a liquor retailer with a similar demographic, the retail pricing structure (without SLT) was binned into the four price categories of Well, Call, Premium, and Super Premium.  The products within these four price categories were then compared to a venue of similar demographics which had their bar selection and pricing online.  Taxes, credit card charges, etc. were later included in the business model, however, for the purposes of forecasting taxes were not included.

The result of the web-scraped analysis crossed 11,692 products across 12 liquor-related groups (*Liquerus/Cordials, Tequila, Beer, Cider, Eau de vies, brandies, and other spirits, Gin, Rum, Scotch, Vermouth, Voda, Whiskey, Wine*) for the four price categories of: "Well," "Call", "Premium", and "Super-Premium":
![histogram of liquor distributions](figure/binned_liquors.png)

The tool used for the webscrape, cleaning, and analysis used was Excel 2007.  Once the data was scraped and tidied, then the process of getting to the price per ounce (PPOz) began.  

The process of getting to the per unit cost, **PPOz**, began when all the volumes were converted to ounces.  This includes quantities like "pony keg", "8pk-16oz Cans", "750 mL", etc.  Duplicate products within the same brand (**Brand-Product**) which had several sizes and thus several price points had the highest prices removed as it was assumed that The Dog would only be selecting based upon best pricing for the same Brand-Product.  Eventually 33 additional records were "tossed" because their price point would exceed The Dancing Dog brand and would thus create an outlier.  

Once the conversions were done and the duplicate Brand-Products removed, a **Retail Cost per oz** was calculated by dividing the ounces in the Brand-Product volume by the Retail cost (which did NOT have the Spirits Tax).  Rounding was to two points after the decimal.  This retail cost per ounce was then "binned" in prepration for creating a histogram. 

The logic behind the binning exercise was multi-fold.  First, all calculations were done on a roundup (Ceiling function in Excel) to the nearest nickel (two points after the decimal).  The next logic step eliminated quantities where the price per ounce exceeded $50.00 because this cost would be considered an outlier for The Dancing Dog brand.  After that, if the Retail Cost per ounce was greater than $3.00, then the rounding down was to the nearest dollar (zero points after the decimal), otherwise the rounding was kept at the nickel stage (two points after the decimal).  This was done to reduce the quantity of variations on a price per ounce basis.  There would be few cases within The Dog brand where a greater than $3.00 per ounce price was going to be used. The final step in creating the "bin" was to combine the liquor type from the 12 categories.  

The logic described above for the binning exercise was created only after multiple exploratory analyses were done.  The decision to use variable bin-widths is outlined in this Wikipedia article:
["Using wider bins where the density is low reduces noise due to sampling randomness; using narrower bins where the density is high (so the signal drowns the noise) gives greater precision to the density estimation. Thus varying the bin-width within a histogram can be beneficial."](https://en.wikipedia.org/wiki/Histogram).  Once that was decided the frequencies and the Frequency as a % of total were calculated.  Once the Frequency as a % of the Total was calculated, then the final logical steps of declaring the price point as "Well" (<=25%), "Call" (>25% AND <= 50%), "Premium" (>50% AND <=75%) or "Super Premium" (> 75%) could be implemented.


[frequency of the distributions of the 12 liquor types](figure/frequency_of_distributions.png)

The results of this classification were then returned to the Brand-Product in form of a new designator, "Price Point" and the Brand-Product was then classified as either Well, Call, Premium, or Super Premium.

More importantly though, there was a "Price Point Cheat Sheet" with which the owners of The Dancing Dog could walk around with and review retail pricing with.   This was an important tool for a brand focused on craft and locally-sourced products.  This allowed the owners to walk into a brewery or a distillery, review a menu or a price list, do some quick math to come out with a price per ounce and then place that price point against the sheet.  This would give them the means of seeing if they could position a brand, such as Bombay Sapphire Gin, which is commonly charged at a Premium level when its cost is actually at the Call level.  


![Price Point Cheat Sheet](figure/PricePointCheatSheet.png)



