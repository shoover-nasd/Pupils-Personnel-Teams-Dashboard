# Interventions Management Interface

This repository hosts an interventions management tool authored by North Allegheny School District and built to be compatible with the Ed-Fi Operational Data Store (v3). 

### Short Description
The Interventions Management Interface (IMI) combines basic case management functions and academic data reporting in a simple Power BI template. Districts can use this tool to track student interventions and case notes within an interface that enables drill-throughs to common student warning system metrics, such as individual level attendance and assessment data.

### Contents
#### Overview & Pre-Requisites
- [Project Description (short)](#short-description)
- [Project Description (long)](#long-description)
- [Pre-Requisites Overview](#project-architecture-and-pre-requisites)
#### Full Interface Resources
- [Interface Overview & Setup Instructions](#interface-overview-and-setup)
- [Power BI Template File](https://github.com/shoover-nasd/ed-fi-interventions-management-interface/raw/main/Template%20-%20Interventions%20Management%20Interface.pbit)
- [PowerApps Solution File](https://github.com/shoover-nasd/ed-fi-interventions-management-interface/raw/main/PowerAppSolution%20(Unmanaged).zip)
- [User Instructions]
#### Report-Only Interface Resources (No PowerApps Subscription Required)
- [Report-Only Dashboard Overview](#report-only-dashboard-overview-and-setup)
- [Report-Only Power BI Template File](https://github.com/shoover-nasd/ed-fi-interventions-management-interface/raw/main/PPT%20Interface%20-%20Template%20-%20Parameter%20Updates%20%20(Report%20Only).pbit)
- [Report-Only Setup Instructions (Video)](https://github.com/shoover-nasd/ed-fi-interventions-management-interface/raw/main/Report-Only%20Setup%20Instructions.mp4)
- [Report-Only User Instructions]


### Long Description
The Interventions Management Interface (IMI)--contributed by North Allegheny School District in Pittsburgh, PA--provides a lightweight student data reporting interface that doubles as an interventions and case management tool. The interface uses accessible platforms within the Microsoft environment, and is presented as a Power BI multi-page report with an embedded Power App module leveraging Microsoft’s Common Data Service for a simple model of non-ODS data structures.

Within the interface, users can track student referrals for intervention, pre-referral and during-monitoring interventions, and case notes. For any student in the user district’s Ed-Fi ODS, users can drill through to review a student case profile, an attendance data overview (periodic and daily attendance), and a mini assessment results explorer. The tool also includes an ODS-wide assessment results explorer, allowing users to compare a selected student’s score against the full distribution of student scores on the same assessment.

An anticipated near-term update to the tool will include an academics drillthrough page to show gradebook-level student performance details across courses.

### Project Architecture and Pre-requisites

![Overview Diagram](https://github.com/shoover-nasd/ed-fi-interventions-management-interface/blob/main/Ed-Fi%20Interventions%20Management%20Interface%20Overview.png)

### Interface Overview and Setup
The "out-of-box" interface is presented as a Power BI report which connects to the user district's Ed-Fi ODS and PowerApps environment and offers the features described in [the previous section](#long-description). User districts with the pre-requisites fulfilled (i.e. Power BI, PowerApps/Dataverse licensing, Ed-Fi ODS) can follow the instructions below to deploy the Interventions Management Interface to their environment.

1. [Download the PowerApps Solution File](https://github.com/shoover-nasd/ed-fi-interventions-management-interface/raw/main/PowerAppSolution%20(Unmanaged).zip)
2. [Download the sample intervention types list](https://github.com/shoover-nasd/ed-fi-interventions-management-interface/blob/main/sampleInterventionTypes.csv). If desired, you can clear all rows in the file (except headers) and enter the list of intervention options you want to make available to your users. 
3. Sign into [the PowerApps portal](https://powerapps.microsoft.com/) and navigate to the "Solutions" page using the left-hand menu.
4. Choose "Import solution" from the menu in the top ribbon. Upload the solution file you downloaded to your computer in step 1.
5. Click the solution after it has imported; then click the "PPT_InterventionTypes" component. This will take you to the Dataverse table view for this resource.
6. **Upload pre-set intervention type options**: 
   - Choose "Get Data" from the menu in the top ribbon and select "text/csv" from the list of data source types. 
   - When prompted for a file, upload the sample intervention types CSV you downloaded (and optionally updated) in step 2 and click open/next (note: you may need to copy the file to a directory in your OneDrive account to make it available for upload); then click the "transform data" button to proceed. 
   - Make any desired changes (none should be necessary with the default file from this repository) and click "Next". 
   - In the field mapping window, choose "Load to Existing Table" from the Load Settings menu; select "PPT_InterventionTypes" (it may have a "cr59c_" prefix or similar) from the destination tables drop-down menu. 
   - Use the Source field drop-down menus to map each field to the field with a corresponding name in the destination table (or click the "Auto map" button in the top-right corner) and click "Next". 
   - Select "Refresh manually" from the Refresh Settings page unless you plan to update and sync intervention options from the same file (not supported through these instructions but certainly an option). 
   - Click "create" to load the data into your solution environment.
8. [Download the Power BI template file](https://github.com/shoover-nasd/ed-fi-interventions-management-interface/raw/main/Template%20-%20Interventions%20Management%20Interface.pbit) and open it on your desktop.
9. Enter the connection string parameters as prompted. The first should be the server name where your ODS is hosted. The second should be the ODS database you wish to connect to. The third should be your PowerApps environment URL (you can find this in the PowerApps admin center).
10. Delete the PowerApps visual in the center of the screen. Replace it by inserting a new, blank PowerApps visual from the visualizations menu on the right-hand side.
11. Click the new PowerApps visual, and, before clicking anywhere else on the visual, add the following data fields (listed here as TableName>>FieldName) **in this order**: DimStudent>>FullName, DimStudent>>Grade, DimStudent>>PPTReferral, DimStudent>>StudentUSI, DimPPTCase>>cr59c_caseid, DimPPTCase>>casestatus, DimPPTCase>>casestatus_display, DimPPTCase>>cr59c_ppt_caseid, DimPPTCase>>modifiedon, DimPPTCase>>PPTStatus, DimPPTCase>>ReferralDate, DimPPTReferralReason>>AllReferralDomains. **Click the drop-down for each field to ensure "Don't Summarize" (rather than any aggregation option, like "sum", etc.) is selected, if available. On the drop-down for DimPPTCase>>cr59c_caseid, ensure "Show items with no data" is selected.** 
12. The PowerApps visual should now prompt you to create a new app or add an existing one. Choose "Add" and use the prompts to navigate to the PowerApps environment where you uploaded the solution file from step 4; select the application named "PPT_Notes_App_CDS_Tablet" (may have a numerical suffix). You will be prompted to open and save the app in order to finalize the Power BI data connection; follow the on-screen prompts, which will take you to the PowerApps editor in an internet browser window. From there, open the "File" menu and click "save". After saving, you will have the option to "publish" the app. Click "Publish".
13. Before exiting the PowerApps editor in your browser, open the File menu once more and click "Share". You will be taken to a new page and presented with the option to share with selected users. Add app co-owners and users as appropriate for your use case and click "share." You can then close the window and return to Power BI.
14. Click the "Modeling" tab on the top ribbon and select "Manage Roles" to configure your row-level security for the data model. If your use case requires school-level security groups, you can simply replace the security group names and rules that are included by default with the relevant school names for your district. Optionally, consult [Microsoft's documentation](https://docs.microsoft.com/en-us/power-bi/admin/service-admin-rls) for more information on row-level security configuration options.
15. *(Optional)* Make any desired modifications to the report in the Power BI Desktop interface.
16. Click the "Home" tab on the top ribbon, then click the "Publish" button to push the report to your Power BI online environment.
17. Open a web browser and navigate to the workspace where you published the report. You will see two rows with the report name you published--one representing the report itself, the other representing the dataset that sits behind the report. Find the row with the dataset for your report (red, database icon), click the three dots to open the options menu, and choose "Security."
18. On the security page, click through each security group and add users as desired. *Note: if you have already configured sets of school-based users as M365 groups, for example, you can type the group name to add all members at once.*
19. Navigate back to the workspace for your report, then click the link to the report itself (i.e. the row with the report name and a blue icon with data bars).
20. On the top ribbon, click the "Share" button to share your report with desired users. Notes:
    - Users will only see data that is permitted according to the security group they are members of.
    - Users who are not in any security group but have been shared on the report will not be able to see any visuals.
    - Users who will interact with the embedded case managament PowerApp must also (separately) be given permission to access the application *(see step 13)*.

### Report-Only Dashboard Overview and Setup
Districts without a full PowerApps & Dataverse (formerly Microsoft Common Data Service) subscription can take advantage of a pared-down version of the interface. This "report-only" interface includes all report pages from the full version which do not depend on the interventions management application component. Currently, this includes student-level attendance data, student-level assessment data, and an all-student assessment results explorer page. North Allegheny staff plan to continue updates to the available report pages as the district's Ed-Fi Implementation progresses to include more data domains.

Click the links below to...
- [Download the Report-Only Power BI Template File](https://github.com/shoover-nasd/ed-fi-interventions-management-interface/raw/main/PPT%20Interface%20-%20Template%20-%20Parameter%20Updates%20%20(Report%20Only).pbit)
- [View Setup Instructions](https://github.com/shoover-nasd/ed-fi-interventions-management-interface/raw/main/Report-Only%20Setup%20Instructions.mp4)
- [View User Instructions]

## Legal Information

Copyright (c) 2021 Ed-Fi Alliance, LLC and contributors.

Licensed under the [Apache License, Version 2.0](LICENSE) (the "License").

Unless required by applicable law or agreed to in writing, software distributed
under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR
CONDITIONS OF ANY KIND, either express or implied. See the License for the
specific language governing permissions and limitations under the License.

See [NOTICES](NOTICES.md) for additional copyright and license notifications.
