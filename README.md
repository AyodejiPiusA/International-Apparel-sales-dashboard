Project Name: International Apparel Sales Dashboard
Tools: Microsoft Excel (Pivot Tables, Slicers, Dashboarding)
Objective: Visualize sales trends, product performance, and total revenue health while handling data anomalies (Shipping/N/A sizes).

1. DATA PROCESSING & CLEANING
	i. Separation of "Good" vs. "Bad" Data
		* Initial Audit: The raw dataset was analyzed for completeness. Rows were detected to have missing or irregular values in the SKU and Size columns.
		* Segregation: The dataset was split into two working subsets: "Good Data" which are rows with perfect matches (Valid SKUs, Standard Sizes) and "Bad Data" 				which are rows containing errors, missing SKUs, shipping fees mislabeled as products, or non-standard formatting.

	ii. The Cleaning Process
		* SKU Generation: Rows where the SKU was missing but a Product Name existed were identified and i performed a reverse-lookup against the 					Master Product List to retrieve and populate the correct SKUs for these missing rows.
		
		* Size Standardization: Many rows had empty Size fields or contained irrelevant metadata in the Size column. For items with known SKUs but missing sizes, i 				cross-referenced the inventory list to assign the correct size. For non-product line items (like "Shipping Fees"), i labeled the Size as "N/A" as this prevents these rows from appearing as 		Blanks in the charts while ensuring their Revenue values are preserved for the Total Revenue.

	iii. Data Unification
		* Reconstruction: Once the "Bad Data" subset was cleaned and standardized, it was attached back to the "Good Data" subset. These two subset were merged into a single 				"good data" source. I also verified that the Total Revenue of the new "good data" matched the sum of the original raw data this ensures no money was lost 				during cleaning.

	iv. Final Formatting
		* Dates: I converted text-based date strings into valid Excel Date formats to enable Timeline Slicing.
		* Currency: I Formatted GROSS AMT columns to $ to ensure accurate visualization in KPIs.


2. The Pivot Tables
	* Location: All Pivot Tables are stored on the Pivot Tables sheet which contains key tables such as;
		* KPI_Revenue & KPI_Quantity: Single-cell pivots used solely to feed the Dashboard header cards.
		* Sales_Trend: Groups data by Months for the timeline view.
		* Best_Sellers: Filtered to show top products.
		* Size_Demand: Filtered to exclude "N/A"/"Unknown".
		* Top_Customers: which shows the top 10 overall customers.

3. Dashboard Architecture
	* Layout: It consist of the side bar and the main charts
		* Sidebar (Left): Anchored the primary filters while the KPIs are just located right above that to ensure the details are viewed directly while filtering.
		* Main Charts (Right):  Contains detailed trends and breakdowns.

	* KPI Cards were constructed using Linked Shapes. Blue rectangles are linked directly to bridge cells in the Pivot sheet and Labels ("TOTAL REVENUE") are separate text boxes grouped with the shapes.

	* Slicers: consist of;
		* Month Slicer: Connected to all charts except the sales trend chart and all KPIs.
		* Size Slicer: Connected to all charts but except the size demand chart and all KPIs. This allows specific product filtering without erasing the "Total Company Revenue" context and The 		"Visual Cheat" was applied to the Size Slicer to hide empty "N/A" buttons by resizing the slicer window.

4. Security Protocol: The sheet is Protected. Users can only click Slicers. All charts, shapes, and cells are locked to prevent accidental deletion or misalignment.


5. BUSINESS VALUE & KEY INSIGHTS
	1. Problems Solved
		* Revenue Blindness: . This dashboard separates Product Revenue from Operational Fees (Shipping). Previously, total revenue was a static number
		* Inventory Guesswork: By visualizing the Size Demand (Qty Sold by Size), I eliminate guessing which sizes to restock.  We now know exactly which variations drive volume versus which 			ones sit on the shelf.
		* Seasonality Visibility: The 12-Month Trend Line replaces gut feelings about "slow months" with hard data, revealing specific peaks i.e May/October and troughs to plan for.
	
	2. Recommendations
		* Inventory Planning:
			* Increase stock depth for Top 3 Best Sellers (visible in the "Best Sellers" chart) by 20% ahead of peak months identified in the Trend Chart.
			* Reduce procurement of "Bottom 3" sizes to free up cash flow, as the Size Analysis shows these account for <5% of volume.

		* Marketing Focus:
			* During low traffic months (dip in Trend Line), launch targeted promotions on the "Best Sellers" to artificially boost revenue, rather than discounting low-demand 			items that customers don't want.

