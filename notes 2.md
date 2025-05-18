Okay, I understand this "free bag scheme" for retailers. It's a volume-based incentive where retailers receive a specific number and type of free bags based on the total metric tonnes of specified products they purchase from distributors during the scheme period. The scheme has defined slabs and an additional rule for volumes exceeding a certain threshold (e.g., beyond 4MT).

Your current verification checks are solid for confirming the accuracy of data entry and individual calculations within PQR for this scheme. Now, let's outline the macro-level checks that can provide a broader view and help catch errors over time and in connection with business operations.

**I. Trend Analysis and Anomaly Detection (Time-Series Based)**

These checks help identify deviations from expected patterns in how free bags are being distributed.

1.  **Total Number of Free Bags Disbursed (by type and size):**
    * **Check:** Track the total quantity of each specific free bag (e.g., "5kg of WC," "10kg of WC") disbursed per scheme, per product involved in the purchase, per area, and per retailer type over multiple scheme periods.
    * **How it provides a macro view:** Gives an overview of the "cost" in terms of inventory for this scheme.
    * **Potential Errors Caught:**
        * A sudden surge in a particular free bag type might indicate an error in PQR logic for a specific slab or incorrect product mapping for the incentive.
        * If the total number of free bags is unexpectedly low despite high sales, PQR might not be triggering eligibility correctly.
        * Errors in scheme setup where the wrong free bag product or size is assigned.
    * **Example:** If typically 1000 bags of "5kg WC" are given out for "Scheme Summer_Retail," but this time it's 10,000 bags without a corresponding 10x increase in eligible retailers or their purchase volumes, it's a red flag for PQR calculation or setup error.

2.  **Average Number of Free Bags per Eligible Retailer:**
    * **Check:** Calculate and track the average number of free bags (total, or by specific type) received by retailers who qualified for the scheme.
    * **How it provides a macro view:** Helps to see if, on average, retailers are receiving a consistent level of incentive, or if there are unexpected shifts.
    * **Potential Errors Caught:**
        * If the average suddenly jumps or drops, it could indicate that PQR is incorrectly assigning retailers to slabs or miscalculating the quantity of bags for the "additional MT" rule.
        * Errors in how PQR aggregates total purchase volume for a retailer to determine their slab.
    * **Example:** If retailers qualifying for incentives usually get an average of 3 free bags, and this suddenly changes to an average of 1 bag or 10 bags, it suggests a systemic issue in PQR's slab assignment or incentive calculation.

3.  **Number of Retailers Qualifying per Slab:**
    * **Check:** Track the number of retailers falling into each defined purchase volume slab (e.g., 0.75-1 MT, 1-2 MT, etc., and those qualifying for the "additional MT" rule) over time.
    * **How it provides a macro view:** Shows if the distribution of retailers across slabs is consistent or if there are unexpected shifts, which could point to data or logic errors.
    * **Potential Errors Caught:**
        * Incorrect slab definitions entered into PQR (e.g., 0.75-1 MT entered as 0.75-10 MT).
        * Errors in PQR's logic for assigning retailers to slabs based on their total volume.
        * Issues with the sales data feed if volumes are consistently misreported, pushing retailers into wrong slabs.
    * **Example:** If the "0.75-1 MT" slab usually has 500 retailers, but suddenly has only 50, while the next slab up sees a massive increase, it could indicate an error in the boundary condition of the first slab in PQR.

4.  **Frequency of "Additional MT" Rule Trigger:**
    * **Check:** Specifically monitor how many retailers qualify for the "beyond 4MT, for every additional 1 MT sold..." rule and the total number of free bags disbursed under this specific rule.
    * **How it provides a macro view:** This rule is different from fixed slabs, so monitoring its application separately is important.
    * **Potential Errors Caught:**
        * Errors in PQR's logic for calculating "additional MT" (e.g., counting every 0.5 MT instead of 1 MT, or miscalculating the number of extra bags).
        * Incorrect threshold (e.g., applying it beyond 3MT instead of 4MT).
        * PQR failing to apply this rule when it should, or applying it when it shouldn't.
    * **Example:** If no retailers ever seem to qualify for the "additional MT" rule despite individual high volumes being reported, the logic in PQR might be broken. Conversely, if almost everyone qualifies with many extra bags, the threshold or calculation might be erroneously low.

**II. Cross-System Data Validation and Integrity**

Ensuring the data PQR uses matches other key business systems.

5.  **Retailer Sales Volume Reconciliation (Distributor to Retailer):**
    * **Check:** Your team checks "total sale in Metric tonnes calculated in scheme via PQR." Expand this by reconciling the *sales volume attributed to each retailer in PQR* with sales data reported by distributors for those retailers for the specified products and period. This is more complex as it involves data from distributors. If your company captures distributor-to-retailer sales data, this is highly valuable. If not, this check might be limited to overall distributor sales of those products.
    * **How it provides a macro view:** Validates the core transactional data upon which retailer eligibility is based.
    * **Potential Errors Caught:**
        * Discrepancies in sales data reported by distributors versus what's used in PQR.
        * Errors in PQR aggregating sales from multiple distributors to a single retailer (if applicable).
        * Incorrect product mapping – ensuring only "Products Involved" are counted.
    * **Example:** PQR shows Retailer R bought 1.5 MT from Distributor D1 and D2 combined (of scheme products). You would try to verify this against reports from D1 and D2 regarding their sales to Retailer R.

6.  **Retailer Master Data Consistency:**
    * **Check:** Similar to the distributor scheme, periodically compare retailer attributes used by PQR (Retailer ID, linked Distributor, Area, State, Customer Type, Included/Excluded status) against your central retailer database or CRM (if one exists that tracks retailers).
    * **How it provides a macro view:** Ensures correct retailer identification and categorization for scheme eligibility.
    * **Potential Errors Caught:**
        * Incorrect retailer linkage to distributors affecting data aggregation.
        * Outdated retailer status (e.g., closed retailer still shown as active and receiving incentives).
        * Misclassification of retailer type, area, or state leading to wrong scheme application or exclusion.
    * **Example:** A retailer is marked as "Excluded" in your master list but is still processed and receives free bags via PQR.

7.  **Free Bag Product Master Data Check:**
    * **Check:** Verify that the "Products" designated as free bags (e.g., "WC") and their specified "sizes" (e.g., "5kg," "10kg") in PQR's scheme setup match active, existing SKUs in your product master/inventory system.
    * **How it provides a macro view:** Prevents schemes from promising non-existent or incorrectly coded free items, which would cause downstream fulfillment issues.
    * **Potential Errors Caught:**
        * Scheme set up in PQR to give away a discontinued bag size or product.
        * Typographical errors in the product code or size of the free bag in PQR.
    * **Example:** The scheme in PQR is set to give "7kg of WC," but your company only produces "5kg of WC" and "10kg of WC."

**III. Scheme Parameter and Logic Integrity (Over Time)**

Ensuring the scheme rules are consistently and correctly applied.

8.  **Slab Definition Consistency:**
    * **Check:** For recurring free bag schemes or similar ones, compare the volume slab definitions (e.g., "Greater than or equal to," "Less than" values for each slab) and the corresponding free bag entitlements in PQR over different periods.
    * **How it provides a macro view:** Catches unintentional changes in scheme structure.
    * **Potential Errors Caught:**
        * Accidental changes to volume thresholds for slabs.
        * Errors in data entry when setting up a new iteration of a similar scheme, leading to different slab boundaries or free bag quantities than intended.
        * Inconsistent definition of boundaries (e.g. "Less than 1 MT" vs "Less than or equal to 1 MT" if the intent is specific and PQR has options).
    * **Example:** Slab 3 (0.75 to 1 MT) always gave "2 bags of 5kg WC + 1 bag of 10kg WC." In the current PQR setup for the same scheme name, it mistakenly shows only "1 bag of 5kg WC."

9.  **"Boundary Condition" Retailer Analysis (Aggregate):**
    * **Check:** Analyze if an unusually high number of retailers have purchase volumes falling *exactly* at the boundaries of the defined slabs (e.g., exactly 0.75 MT, 1.0 MT).
    * **How it provides a macro view:** Similar to the distributor scheme, extreme clustering can highlight PQR rounding issues or sensitive points in the volume data.
    * **Potential Errors Caught:**
        * Rounding logic in PQR that might be pushing retailers just into or out of a slab incorrectly.
        * Potential for data feed issues where volumes are being rounded before reaching PQR.
    * **Example:** A large number of retailers are recorded with exactly 0.749 MT, just missing the 0.75 MT threshold for Slab 3. This could be legitimate, or it could indicate a rounding down issue in PQR or the source data.

**IV. Inventory and Cost Impact Checks (from a Verification Standpoint)**

While your team doesn't make business decisions, you can flag potential errors in PQR that have significant inventory or (indirectly) cost implications.

10. **Total Value/Volume of Free Goods Disbursed:**
    * **Check:** Estimate the total inventory volume (in MT or KG) and, if possible, the cost value of all free bags disbursed for a scheme. Track this trend.
    * **How it provides a macro view:** Provides a sense of the scheme's "cost" in terms of goods. A sudden unexplained spike could indicate an error in PQR leading to over-disbursement.
    * **Potential Errors Caught:**
        * PQR errors that lead to a much higher quantity of free bags being awarded than intended by the scheme design (e.g., a typo awarding 20 bags instead of 2).
        * The "additional MT" rule being applied too generously due to a logic flaw.
    * **Example:** If the cost of free bags for a scheme usually averages Rs. 200,000 and it jumps to Rs. 1,000,000, PQR might be erroneously awarding five times the intended free bags.

11. **Ratio of Free Goods to Purchased Goods:**
    * **Check:** Calculate the ratio of the total volume (MT/KG) of free bags given out to the total volume (MT) of "Products Involved" purchased by qualifying retailers under the scheme. Track this ratio over time.
    * **How it provides a macro view:** This normalizes for overall sales activity. A significant change in this ratio would be a strong indicator of a PQR calculation error.
    * **Potential Errors Caught:**
        * Errors in PQR's logic for determining eligibility or the quantity of free bags, leading to a disproportionate amount of free goods compared to purchases.
    * **Example:** If for every 100 MT of products sold, 1 MT of free bags is typically given, and this ratio suddenly changes to 5 MT of free bags per 100 MT sold, there's likely an error in PQR's incentive calculation.

**V. Process and Documentation Checks**

12. **Clarity of Scheme Input Documentation:**
    * **Check:** Review the source documents (like the image you provided) that define the scheme before it's entered into PQR. Are the slabs, free bag types, sizes, quantities, and rules (like the "additional MT" rule) clear and unambiguous?
    * **How it provides a macro view:** Ambiguity in definition is a common source of data entry or logic errors in PQR.
    * **Potential Errors Caught:**
        * Misinterpretation of scheme rules by the person configuring PQR, stemming from unclear original instructions.
    * **Example:** If the source document for the "additional MT" rule is vaguely worded, it could be implemented differently in PQR than intended.

By implementing these macro checks, your verification team can significantly enhance its ability to catch errors that might be missed when only looking at individual transactions. This provides a safety net to ensure the "free bag scheme" is operating as intended from a broader operational and data integrity perspective.
