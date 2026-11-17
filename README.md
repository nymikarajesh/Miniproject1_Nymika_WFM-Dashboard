# Miniproject1_Nymika_WFM-Dashboard

Calendar =
ADDCOLUMNS(
    CALENDAR(MIN(Data[Date]), MAX(Data[Date])),
    "Year", YEAR([Date]),
    "Quarter", "Q" & QUARTER([Date]),
    "MonthNo", MONTH([Date]),
    "Month", FORMAT([Date], "MMM")
)

Offered = SUM(Data[offered_Volume])
Handled = SUM(Data[handled_Volume])
Abandoned = SUM(Data[abandoned_Volume])
Abandon Rate = DIVIDE([Abandoned], [Offered])
Service Level % =
    DIVIDE(SUMX(Data, Data[Service_Level_Percent] * Data[offered_Volume]), [Offered]) / 100
Avg Wait (s) =
    DIVIDE(SUMX(Data, Data[Wait_Time_Avg] * Data[offered_Volume]), [Offered])
AHT (s) =
    DIVIDE(SUMX(Data, Data[aHT_Seconds] * Data[handled_Volume]), [Handled])
Occupancy % =
    DIVIDE(SUMX(Data, Data[Occupancy_Percent] * Data[offered_Volume]), [Offered]) / 100
Avg Required FTE = AVERAGE(Data[required_FTE])
Avg Active Agents = AVERAGE(Data[Active_Agents])
Staffing Gap = [Avg Active Agents] - [Avg Required FTE]
SL Target = 0.8
Visual	Fields	Notes
Slicers ×6	Calendar[Year], Data[Region], Data[Channel], Data[Business_Unit], Data[ASU_Tier_Filter], Data[All_Units_Filter]	Year and Channel as Tile style; Region as Tile; Business Unit as Dropdown. Turn on multi-select.
Card ×7	Offered, Handled, Abandon Rate, Service Level %, Avg Wait (s), AHT (s), Occupancy %	Use the Card (new) visual to show a reference label. Turn category labels on.
Line chart	X: Time hierarchy. Y: Offered, Handled	Enable drill-down arrows on the visual; title "Offered vs handled volume over time".
Donut chart	Legend: Channel. Values: Offered	Detail labels: category + percentage. Three slices only.
Clustered bar	Y: Geography hierarchy. X: Offered	Filters pane → Top N = 10 by Offered. Use the drill-down arrow to go Region → Country → Site.
Clustered column	X: Business_Unit. Y: Abandon Rate	Sort descending; data labels on; Y axis as %.
Line chart	X: Data[Hour]. Y: Service Level %, SL Target	Format SL Target as a dashed line. Y axis from 60% to 100%.
Clustered column	X: Region. Y: Avg Required FTE, Avg Active Agents	Two series, so keep the legend on.
Table	Queue_Name, Offered, Abandon Rate, Service Level %, Avg Wait (s), AHT (s), Occupancy %	Add Conditional formatting → Data bars to Offered; background colour scale on Abandon Rate.
