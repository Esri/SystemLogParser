# System Log Parser
## Version 0.12.17.0
### Date: 2022/09/08

-------------------------------
![System Log Parser GUI](/assets/images/SystemLogsGUI_ArcGISServer_web_small.png)
-------------------------------

#### Description 
System Log Parser is an ArcGIS for Server (10.1+) log query and analyzer tool to
help you quickly quantify the GIS usage in your deployment.
When run, it connects to an ArcGIS for Server instance on port 443/6443/6080/80 as a publisher
(or an administrator), retrieves the logs from a time duration (specified as an input),
analyzes the information then produces a spreadsheet version of the data that
summarizes the service statistics.
However, System Log Parser can also read access logs from other sources such as:
Microsoft IIS, Apache Tomcat, Amazon ELB/ALB, Amazon CloudFront and Microsoft Azure.
The command-line version of System Log Parser (slp.exe) is used by the current releases of 
ArcGIS Monitor for data capture.

### Download Latest Release
[System Log Parser Download](/binaries/latest/SystemLogParser.zip)

#### System Requirements
- 64bit Windows Operating System:
	- Windows (Workstation): 7, 8*, 8.1**, 10**
	- Windows (Server): 2008, 2012, 2016, 2019, 2022
- Processor: AMD64/Intel64
- RAM: 8GB
 - Disk Space: 2GB free when using the new Optimized Analysis Type 
 - Security Protocol***: TLS 1.0, TLS 1.1, TLS 1.2, or TLS 1.3
 - Microsoft .NET Framework 4.8 (Full)
 - Publisher (or administrative) access to ArcGIS Server's REST API Admin endpoint in order to query the logs
 - ArcGIS Server log level set to FINE (from within the ArcGIS Server Manager) before using this tool
 - A deployment running ArcGIS Server 10.1 or higher
 - If performing Web (IIS) log analysis, it is recommended to have the Log File Rollover Schedule set to Hourly or Daily (from the Internet Information Services Manager)

 - *If using Windows 8, .NET Framework 3.5 (in addition to 4.8) must be enabled per Microsoft documentation
 - **If using Windows 8.1 or Windows 10, .NET Framework 3.5 (in addition to 4.8) must be enabled per Microsoft documentation
 - ***Not relevant if logs are consumed directly from the file system (e.g. reading the local disk or via CIFS share)

#### System Recommendations:
 - Microsoft Excel 2010 or higher (or appropriate xlsx viewer)
 - RAM: 16GB
 - Disk Space: 6GB free when using the new Optimized Analysis Type 
 - Security Protocol*: TLS 1.2 or TLS 1.3
 - If performing Microsoft IIS log analysis, it is recommended to have the Log File Rollover Schedule set to Hourly (from the Internet Information Services Manager); Hourly creates more, smaller files but allows for a finer grain search 
 - If querying through the web, an user with administrative access is recommended as they can gather details on all service types
 - *Not relevant if logs are consumed directly from the file system (e.g. reading the local disk or via CIFS share)

-------------------------------
#### Esri Community Articles on Using System Log Parser 
- [ArcGIS Enterprise Analysis with System Log Parser's Optimized Analysis Type](https://community.esri.com/t5/implementing-arcgis-blog/arcgis-enterprise-analysis-with-system-log-parser/ba-p/1189005)
- [Automating System Log Parser from the Windows Command Line](https://community.esri.com/t5/implementing-arcgis-blog/automating-system-log-parser-from-the-windows/ba-p/1195294)
- [ArcGIS Enterprise Analysis with System Log Parser's ServiceDetails Analysis Type](https://community.esri.com/t5/implementing-arcgis-blog/arcgis-enterprise-analysis-with-system-log-parser/ba-p/1198115)
- [System Log Parser - Statistics and Service Optimization](https://community.esri.com/t5/implementing-arcgis-blog/system-log-parser-statistics-and-service/ba-p/886389)
- [ArcGIS Server Tuning and Optimization with System Log Parser
](https://community.esri.com/t5/implementing-arcgis-blog/arcgis-server-tuning-and-optimization-with-system/ba-p/886361)
-------------------------------

##### CHANGELOG

Build 0.12.17.0 (Prerelease)
1. Added a listing of the IsSchemaLocking property for each service (where is exists) on the "Site Details" worksheet; This worksheet is found through: the ServiceDetails Analysis Type, enabling the "Add Service Details to Report (Enhanced Site Report)" option in the GUI, or setting the "-esr" parameter to true on the command-line; This worksheet is not available with the Optimized Analysis Type

Build 0.12.16.0 (Prerelease)
1. Added Wait Time and Instance Creation Time statistics to the TextFile report
2. Fixed an issue with the JSON Report Type where the complete output would not be available
3. Corrected a typo on the command line help where the JSON Report Type was listed as an Analysis Type 
4. Added Wait Time and Instance Creation Time statistics to the JSON report

Build 0.12.15.0 (Prerelease)
1. Added the Optimized Analysis Type as an option for AGS -- ArcGIS Server Log Query (Web); this is the recommended Analysis Type as the memory savings over Simple, WithOverviewCharts and Complete reports is significant; an increase in performance might be minimal as the ArcGIS Server Admin API will most likely be a bottleneck in the speed 
2. Updates to the command line help (show help with "slp.exe -h" or "slp.exe -help")
3. Changed the GUI button "Analyze Logs" to just "Analyze"

Build 0.12.14.2 (Prerelease)
1. When generated an enhanced site report, SLP skips over the examination of service datasources that cannot be parsed
2. Added several internal checks to avoid crashes by SLP when the siteDetails.ArcGISServiceDatasourceDetails object contains unexpected data
3. Increased the apploglevel verbosity of several internal methods

Build 0.12.14.1 (Prerelease)
1. Package was unable to include signed binary files created by Esri; this has been corrected

Build 0.12.14.0 (Prerelease)
1. If System Log Parser was generating "enhanced site report" worksheet, the reading of the site configuration data could be interrupted if "corrupt service" was encountered; slp now tries to continue if such a condition is met
2. Added some details to the application debug log on timezone and utc offset from the machine running System Log Parser
3. Added an Analysis Type of ServiceDetails which only connects to the ArcGIS web endpoint to retrieve service and datasource information (e.g. no log statistics)
4. Added comments to the Min Instances (Node) and Max Instances (Node) colummn headers on the "Site Details" worksheet; comments are to clarify that although some DMaps (Shared) and SDS (Hosted) services may contain a configuration with an unexpected instances value, it has not impact to the respective service
5. Provided an update to the Get-SLPReport.ps1 PowerShell automation script; this script can be used to quickly download large amounts (e.g. 1 month) of (ELB) log data using multiple copy threads in parallel (outside of SLP), then SLP is invoked to read all the log data from the local disk and quickly create an Optimized report

Build 0.12.13.0 (Prerelease)
1. Added the version of System Log Parser to the "Summary" worksheet
2. Added "Start Time for Query (Coordinated Universal Time)" and "End Time for Query (Coordinated Universal Time)" to the "Summary" worksheet
3. For clarity, the "local time" string in the "Summary" worksheet was changed in "Start Time for Query (local time)" and "End Time for Query (local time)" to the actual local zone name of where System Log Parser is being run
4. In the Service Provider Stats table ("Summary" worksheet) for the "Hosted (SDS)" row, the "Minimum Instances Per Node (Started)" and "Maximum Instances Per Node (Started)" values have been set to 0 despite their actual definition; this was done to avoid confusion; in some cases, a hosted feature service can take a value for this option but in actuality, it has no affect on the service
5. In the Service Provider Stats table "Summary" worksheet for the "Shared ArcGIS Pro (DMaps)", the "Minimum Instances Per Node (Started)" and "Maximum Instances Per Node (Started)" values have been set to Site value for the Shared Instance Setting (e.g. Number of shared instances per machine)
6. Corrected an incorrect labeling of the file and product version for the SystemLogsGUI executable

Build 0.12.12.0 (Prerelease)
1. Added a Service Provider Stats table to the "Summary" worksheet

Build 0.12.11.2 (Prerelease)
1. Fixed issue when parsing ArcGIS Server logs from the file system where incomplete entry would stop SLP from reading the rest of the files

Build 0.12.11.1 (Prerelease)
1. Fixed issue when parsing IIS logs where SLP could crash if the header and data column count did not match on a line and if an Optimized report was being created

Build 0.12.11.0 (Prerelease)
1. For ArcGIS Server (web) log queries that have the "Add Service Details to Report" option selected (also known as the enhanced site report option), the ArcGIS "provider" field is listed for each service on the "Site Details" worksheet

Build 0.12.10.2 (Prerelease)
1. Fixed a performance issue with the "Arrival Rate" worksheet for WithOverviewCharts and Complete reports
2. Fixed an issue the "Arrival Rate" worksheet for WithOverviewCharts and Complete reports (ArcGIS Server log queries) where under some conditions the displayed data object could still exceed the maximum of rows allowed in the table
3. To help keep the file size more manageable for WithOverviewCharts and Complete reports (ArcGIS Server log queries), the maximum table size of the "Arrival Rate" worksheet is now set to 200,000 rows
4. Minor fixes to application debug log statements

Build 0.12.10.1 (Prerelease)
1. Fixed an issue with the Optimized report on "Statistics By Resource" worksheet where if the listed Methods ended the word "Server", the word "Server" would be omitted
2. Fixed a presentation issue with the "Elapsed Time - All Resources" worksheet where the Epoch Time values would be formatted with a comma
3. Fixed issue with the "Arrival Rate" worksheet for WithOverviewCharts and Complete reports (ArcGIS Server log queries) where the number of items in the table could exceed the maximum allowable for a spreadsheet and crash System Log Parser; the table will now automatically cutoff the remaining data at 1,000,000 rows
4. Adjusted the "Request Throughput" worksheet for optimized reports to show Minutes if the available data time span is 24 hours or less; if over 24 hours, the worksheet will instead show throughput across Hours

Build 0.12.10.0 (Prerelease)
1. Fixed an issue with the Optimized report for ArcGIS Server file system log queries where long timespans (or very busy Sites) would contain enough data for the "Arrival Rate" worksheet that exceeded the maximum table size in Excel; the maximum number of rows for tables in the Optimized report is set to 200,000
2. For the Optimized report, the "Client IP", "Users", "Wait Time (Queue Time)", "Instance Creation Time" and "Request Throughput" worksheets have a maximum number of rows for tables set to 200,000
3. slp.exe now prints an error message if an ArcGIS Server (web) log query is used with the Optimized Analysis Type; currently the only "ArcGIS Server" log query that is supported with the Optimized Analysis Type is "File System"
4. Fixed issue with the "Request Throughput" worksheet where it would show Minutes insteads of Hours; this was greatly increasing the size of the report; Minutes are only supposed to be shown for query spans less than or equal to 3 hours
5. Added option to slp.exe called "-optimizedextras" which can toggle the inclusion of some of the worksheets; the specific worksheets are: Client IP, Users, Arrival Rate, Wait Time (Queue Time), Instance Creation Time; some of the table contents for these worksheets can grow very large as the presentation is not a statistic view of the data; this option allows you to omit them in order to use less memory when performing large queries
6. Increased the application debug log verbosity for some functions
7. Updated the slp.exe command-line Help
8. Adjusted the logic for handling the log source directory path(s) for ArcGIS Server file system log queries (Optimized, Simple, WithOverviewCharts, or Complete reports)
9. Minor formatting adjustments of the "Request Throughput" worksheet

Build 0.12.9.0 (Prerelease)
1. Removed the elb.exe and elb.exe.config files from the System Log Parser package; these files were kept for backwards compatibility to support early versions of ArcGIS Monitor extensions; the slp.exe (and slp.exe.config) provides the same functionality and support

Build 0.12.8.0 (Prerelease)
1. Minor adjustments to the reading concurrency logic for Optimized Analysis Type IIS log queries
2. Added the Optimized Analysis Type as an option for AGSFS (ArcGIS Server File System) log queries; this is the recommended Analysis Type as the memory savings and performance increase over Simple, WithOverviewCharts and Complete reports are significant
3. Minor adjustments to the column descriptions on the "Wait Time (Queue Time)" and "Instance Creation Time" worksheets for IIS log queries using an Analysis Type of "WithOverviewCharts" or "Complete"
4. Added column description detail to the "Arrival Rate" worksheet for AGS (web) and AGSFS log queries (Analysis Type of WithOverviewCharts and Complete); this was done to match the "Arrival Rate" worksheet from the new Optimized Analysis Type
5. For AGS (web) and AGSFS log queries, the "Arrival Rate" worksheet, a label is appended to the end of the table noting that the arrival of hosted service requests can be pulled from the logs but their respective elapsed time information is not found on the "Statistics By Resource" worksheet
6. The Optimized Analysis Type is now the default for ArcGIS Server (FS) log queries from the GUI

Build 0.12.7.1 (Prerelease)
1. Removed several command-line options that were utilized to support ArcGIS Monitor (Classic) functionality 
2. Added logic for elbfs log queries to skip files of zero size
3. Fixed an issue where querying IIS logs from the GUI did not fully take advantage of the all the memory improvements of the Optimized Analysis Type; slp.exe (and elb.exe) were not affected by this issue

Build 0.12.7.0 (Prerelease)
1. Fixed issue with Simple, WithOverviewCharts and Complete Analysis Types where HTTP Codes would appear in a non-sorted order
2. Added some small memory savings for Simple, WithOverviewCharts and Complete Analysis Types generated from IIS log queries
3. Added the Optimized Analysis Type as an option for IIS log queries; this is the recommended Analysis Type as the memory savings and performance increase over Simple, WithOverviewCharts and Complete reports are significant
4. The Optimized Analysis Type is now the default for ELB and IIS log queries from the GUI
5. Improved error handling and message verbosity for various log query methods
6. Added fix to automatically remove "info.log" if it was added to the path for ArcGIS Server file system log queries
7. ArcGIS Monitor (Classic) support officially dropped
8. System Log Parser now includes a PowerShell script (Get-SLPReport.ps1) to assist downloading ELB/ALB logs and uncompressing gzip logs outsite of SLP; this adds benefit of using Get-S3Object to quickly download multiple logs simultaneously and then call 7zip directly to uncompress the logs from a script (as oppose having SLP call an external process)
   In this script, the environment inherits credentials from an IAM Role and downloads 30 days worth of logs locally for analysis by SLP
9. Support for calling 7zip as an external process has been removed; see the Get-SLPReport.ps1 script as an example of more securely utilizing a specific release of 7zip for *.log.gz file decompression
10. Added several updates to the command-line Help

Build 0.12.6.0 (Prerelease)
1. For IIS log queries that use an Analysis Type of WithOverviewCharts or Complete, a worksheet called "Service Referer" has been added which lists requested services and the associated referer header along with a count; static "REST", "SOAP", "Portal" and "OtherRequests" are not listed in this worksheet table
2. Added automatic filtering support for the TopographicProductionServer (Topographic Mapping Server) capability; requests for such resources are placed in the (ArcGIS) Server group

Build 0.12.5.1 (Prerelease)
1. System Log Parser executable files (SystemLogsGUI.exe, slp.exe, and elb.exe) include Digitial Signatures with "Environmental Systems Research Institute, Inc." as the Name of signer

Build 0.12.5.0 (Prerelease)
1. Added option to decompress ELB/ALB GNU zip (*.gz) logs with a "local" instance of 7-zip (must be previously downloaded and installed); this feature is only available from the command line (slp.exe) and can be utilized with the "-7zippath [PATH_TO_7ZIP.EXE]" option
2. Added data labels to all charts generated from reports with the WithOverviewCharts or Complete Analysis Type
3. Adjusted the data accuracy presented on the Response and Request Sizes worksheet to 3 decimal places (was 6)

Build 0.12.4.0 (Prerelease)
1. Removed a runtime check that prevented some methods from executing for non-spreadsheet report types
2. Included milliseconds in the app log date timestamps
3. Added the Source Server field to the Optimized report
4. Improved the query statistic collection and display for the Optmized report; a worksheet called, "Query Statistics" is appended to the report if any logs cannot be read
5. Added TRACE as an app log level
6. Some internal code cleanup
7. Added addtional checks for ELB/ALB queries (simple, withoverviewcharts, complete, optimized, downloadlogsonly) to help prevent SLP from stopping in the event it could not read certain logs
8. Added app log verbosity statements to ELB/ALB log queries
9. Added a fix for the command-line (slp.exe) to allow the Report Type of DownloadLogsOnly to override and download logs even if the Analysis Type of Optimized was passed in as an argument
10. Minor updates to the command-line help

Build 0.12.3.0 (Prerelease)
1. Added a new Report Type of "JSON"; this report type option is only available from the command-line (using the "-r json" switch) as the output is printed to the screen (STDOUT)
2. Add the Response Time Histogram summary to the Text Report
3. Minor formatting adjustments to the Text Report
4. Added a fix where System Log Parser would stop reading the logs if entries with a code of 9000 were detected that did not have a service name in the message
5. Adjusted the log filters to better catch errors SEVERE (errors) with a code of 9000
6. Removed the Server IP field as a required column of data for IIS logs; although recommended, it is no longer required
7. Added a fix to address a NullReferenceException that could be encounted when generating an ErrorsOnly report against log entries that were of type SEVERE with a code of 50000

Build 0.12.2.0 (Prerelease)
1. Corrected a display error on the "Wait Time (Queue Time)" and "Instance Creation Time" worksheets where the overall values in the bottom table did not reflect a recent column reordering change
2. Added the "Server Timeout" worksheet for ArcGIS log queries (web and fs, not ageok...no values will be retrieved for ageok reports)
3. Added the "Wait Time Expired" worksheet for ArcGIS log queries (web and fs, not ageok...no values will be retrieved for ageok reports)
4. Fixed some internal reporting logic for ArcGIS Enterprise for Kubernetes (ageok) log queries

Build 0.12.1.0 (Prerelease)
1. Added support for ArcGIS Enterprise on Kubernetes (AGEOK); require version and built of at least: 10.9.1.1357
   Currently, only command-line support exists; to utilize this functionality, pass in "ageok" to the -f command-line switch parameter
   Note: Not all functionality available from AGS is available yet from AGEOK (e.g. "Windows Authentication" and the "Enhanced Site Report") 
2. Minor updates to the command-line help

Build 0.12.0.0 (Prerelease)
1. Updated AWS libraries (AWSSDK.Core, AWSSDK.S3, AWSSDK.IdentityManagement)
2. Updated Azure libraries (Microsoft.Azure.KeyVault.Core, Microsoft.Rest.ClientRuntime, Microsoft.Azure.Storage.Common, Microsoft.Azure.Storage.Blob
3. Removed EPPlus library; added PerfectXL.EPPlus library
4. Updated Newtonsoft.Json library
5. Updated the CommonServiceLocator library
6. Updated the Unity library
7. Updated the NLog library
8. Added support for TLS 1.3
9. The System Log Parser "package" no longer includes the xml file associated with each dll

Build 0.11.3.0 (Prerelease)
1. Added command-line support for AWS ELB/ALB connections through Inherited Role Permissions; under this authentication scenario the Access Key, Secret Key and Region can be omitted from the command line as long as permission is granted to a specific machine using an IAM role and Instance Profile.
   For example, the following could be granted for S3 bucket access (this is not performed from System Log Parser):
   { 
    "Effect": "Allow",
    "Action": [
        "s3:ListBucket",
        "s3:GetObject"
    ],
    "Resource": [
        "arn:aws:s3:::<BUCKETNAME>",
        "arn:aws:s3:::<BUCKETNAME>/*"
    ]
   }

   For more information:
   https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2_instance-profiles.html
   https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html
2. Fixed a formatting issue with the "Request Performance" worksheet
3. Fixed a formatting issue with the "Request Status (HTTP 500)" worksheet
4. For Optimized Analysis Type reports, a "Client IPs" worksheet has been added that lists the IPv4 Addresses and occurrences of connecting machines
5. For Optimized Analysis Type reports, a "Request Throughput" worksheet has been added that lists the number of requests per hour (or per minute if query time span hour component is 3 hours or less)


Build 0.11.2.1 (Prerelease)
1. Fixed an issue when parsing Azure Application Gateway v2 logs where the resource string was taken from requestUri instead of originalRequestUriWithArgs; originalRequestUriWithArgs is favored as it contains the url path that is closer to what the user called
2. Fixed an issue when parsing Azure Application Gateway v2 logs where the resource string included the url parameters; in some cases this would make the resource extremely long and could the log parsing to fail with certain Tile requests
3. Optimized Azure Application Gateway v2 resource analyzer
4. Optimized the VectorTileServer service type definitions

Build 0.11.2.0 (Prerelease)
1. For IIS log queries, any encountered malformed log entries are now just counted and the process is allowed to continue; the malformed log entry count is displayed in the report on the "Summary" worksheet under "Total Malformed Log Entries"
2. Added "Arrival Rate" worksheet (and Request Arrival Time table) for ArcGIS Server (web and file system) log source queries; The Arrival table can help highlight which services might be consistently receiving more requests simultaneously than the available hardware can support; if the service is a tradition one (e.g. dedicated) it may be a good candidate for increasing the ArcSOC instances and/or adding more hardware resources
3. Fixed several formatting issues with the "Throughput per Minute" worksheet
4. The "Statistics By Resource", "Statistics By User", "Wait Time (Queue Time)", and "Instance Creation Time" worksheets are now sorted by Sum; Categorizing the values by Sum helps show which resources are taking the most time overall to work on by the server

Build 0.11.1.1 (Prerelease)
1. Improved support for Azure Application Gateway v2 logs

Build 0.11.1.0 (Prerelease)
1. Added support for Azure Application Gateway log v2
2. Support for ArcGIS Monitor is now deprecated within System Log Parser. The functionality to upload log queries into ArcGIS Monitor will be removed in the near future.
3. When using slp.exe (the command-line version), the ability has been added to override the auto-generated filename of the report through the "-n" switch (e.g. -n "myreport.xlsx")
4. Expanded the regular expressions for ELB and IIS log sources to include group by tilemap and portal content listing requests
5. For AGSFS log queries, any encountered malformed log entries are now just counted and the process is allowed to continue; the malformed log entry count is displayed in the report on the "Summary" worksheet under "Total Malformed Log Entries"
6. For AGSFS log queries, log entries containing the requestID field are now parsed in a safer manner
7. Changed the default spreadsheet column formatting from "auto" to a min and max characters of 5 and 75, respectively; this was done as some columns of data for some sites can have values that are extraordinarily long making the manual adjustment for screen readability cumbersome
8. Several updates to the command-line Help

Build 0.11.0.0 (Prerelease)
1. In the interest of greatly reducing memory requirements (querying busy sites or executing a query with a long time duration) the Analysis Type of "Optimized" has been introduced.
   This new "Optimized" Analysis Type is currently only available for ELB log queries. 
   Memory savings with "Optimized" have been shown to be up to 120 times less than "WithOverviewCharts"! This allows for running "bigger" log queries which cover a longer time span duration (note: the time to download load the logs from the remote source remains the same).  
   The analysis with "Optimized" is also significantly faster than "WithOverviewCharts".
   The "Optimized" report output will be similar to the "WithOverviewCharts" report but not all all worksheets are available.
   The speed and memory savings of the new "Optimized" Analysis Type is achieved by internally transforming the raw log data into a compressed format that is more efficient on system resources to analyze. 
2. Added an automatic filter for tile cache requests for traditional ELB log queries were the resource is rewritten to (more efficiently) just count the calls per map scale

Build 0.10.6.1 (Prerelease)
1. Minor code cleanup and removal of some unused logic

Build 0.10.6.0 (Prerelease)
1. Added additional memory utilization and performance enhancements
2. Adjusted the formatting of the HTTP Method section in the "Summary" portion of the report
3. Fixed issue where some IIS log queries against many large files would result in an "Unhandled Exception: OutOfMemoryException"
4. Added improvements to security for working with passwords in memory at "rest"
5. Adjusted the formatting of the CloudFront section in the "Summary" portion of the report
6. Adjusted the formatting of the HTTP Code section in the "Summary" portion of the report

Build 0.10.5.0 (Prerelease)
1. Added some memory utilization enhancements to various System Log Parser functions
2. Added some format adjustments to the HTTP Code summary sections for both the spreadsheet and textfile reports
3. Added an HTTP Method section to the "Summary" worksheet in the report
4. Added a CloudFront section to the "Summary" worksheet in the report which details some CDN information 

Build 0.10.4.2 (Prerelease)
1. Adding numerical formatting to the integer values of the "Capabilities" worksheet which was missing 
2. Fixed an issue that corrected the reporting on the actual number of HTTP 500 requests for the "Request Status" worksheet if the total exceeded the allowed maximum of 1,000,000
3. The "Throughput per Minute" worksheet has been moved back the "WithOverviewCharts" Analysis Type after additional testing revealed the increase in file size is not drastic; this worksheet enhances the "WithOverviewCharts" analysis while leaving "Complete" to show details on every request

Build 0.10.4.1 (Prerelease)
1. To help keep the file size down for most reports, the "Throughput per Minute" worksheet has been moved back to the "Complete" Analysis Type 
2. Removed some unnecessary formatting in the "Request Status" worksheet

Build 0.10.4.0 (Prerelease)
1. Fixed an issue where floating point numbers would not display properly in a Culture other than "en-US"
2. Increased the verbosity of the System Log Parser application debug log for several methods and objects
3. Fixed an issue where the service requests for the corresponding item in the "Wait Time" workbook would always be listed as 0
4. Fixed a KML request identification issue for System Log Parser to ArcGIS Monitor uploads
5. Fixed an issue that could cause System Log Parser to stop reading malformed ALB logs
6. Added an optimization to elb log queries with a Report Type of "Downloadlogsonly" that the logs are just saved to disk and not also read into memory
7. Added optimizations to elbfs to read all the logs files in the specified directory regardless of file timestamps and to read the log files in parallel
8. Removed the "ArcGIS Capability" stats on the "Summary" worksheet of the spreadsheet and text report 
9. Extended the Analysis Type of "WithOverviewCharts" and "Complete" to include worksheets summarizing requests based on ArcGIS Server Service Types and ArcGIS Server Capabilities
   This new analysis assigns a capability to every request that is based on the requested resource
   For example: MapServer, ImageServer, NAServer, WMSServer, FeatureServer, HostedFeatureServer, VectorTileServer, MapServerDefinition, IMAGESERVERDEFINITION, PortalContentData, REST, OtherRequests, etc...
   These requests are also shown with respect to an ArcGIS Server function capability grouping (availability depends on selected log source)
   For example: ArcGIS Server, ArcGIS Server Extensions, OGC, Tiles, Portal for ArcGIS, Server Definition, REST and SOAP, Other Requests 
10. Extended the Analysis Type of "WithOverviewCharts" and "Complete" to include worksheets summarizing the top 500 slowest requests as well as all HTTP 500 errors (up to the 1,000,000 entries) for the given time span of the query (availability depends on selected log source)
11. Enhanced the HTTP Status information on the Summary worksheet to include details such the specific code as well as its specific definition and number of occurences
12. For easier reading of the spreadsheet report, some worksheet groups were assigned a specific code 
13. The "Throughput per Minute" worksheet has been moved the "WithOverviewCharts" Analysis Type 

Build 0.10.3.2 (Prerelease)
1. Increased the warning message verbosity when an IIS log is read that does not meet the required criteria (e.g. header format, necessary fields) 
2. Fixed an issue in the System Log Parser application debug log that would incorrectly report the number of messages per page (pageSize) returned in the response from ArcGIS Server
3. Fixed an issue with ArcGIS Server (web) queries where an error would be thrown if the hostname of the server contained the same word as the instance name (e.g. arcgis1.mydomain.com:6443/arcgis)  

Build 0.10.3.1 (Prerelease)
1. Provided clarification of the stated Security Protocol requirement; the Security Protocol requirement only pertains to connections over HTTPS and not queries where the logs are consumed directly from the file system (e.g. reading the local disk or via CIFS share)

Build 0.10.3.0 (Prerelease)
1. When using slp.exe (the command-line version), the ability has been added for an ArcGIS Server (FS) query to read from multiple server log directory sources (presumably from the same Site) all at once; the capability can be achieved by wrapping the specified input paths in quotes and separating each ArcGIS Server log folder by a comma, for example: '-i "\\myserver1.domain.com\c$\arcgisserver\logs\MYSERVER1.DOMAIN.COM,\\myserver2.domain.com\c$\arcgisserver\logs\MYSERVER2.DOMAIN.COM"'
2. For ArcGIS Server (FS) queries, fixed an issue with reading certain ArcGIS Server 10.8 log files where the file would contain an xml header but no data; this is a regression bug from versions 0.8.x.x 
3. For TimeSpan queries that exceed 7days with an Analysis Type of "WithOverviewCharts" or "Complete", the "Time" worksheet will now generate charts for the most recent 7days and omit the rest, previous builds will only generate charts of the TimeSpan was 7days or less
4. When using slp.exe (the command-line version), the ability has been added for an IIS query to read from multiple server log directory sources (presumably from the same Site) all at once; the capability can be achieved by wrapping the specified input paths in quotes and separating each IIS log folder by a comma, for example: '-i "\\myserver1.domain.com\c$\inetpub\logs\LogFiles\W3SVC1,\\myserver2.domain.com\c$\inetpub\logs\LogFiles\W3SVC1"'
5. When using slp.exe (the command-line version), the ability has been added for a Tomcat query to read from multiple server logs directory sources (presumably from the same Site) all at once; the capability can be achieved by wrapping the specified input paths in quotes and separating each Tomcat log folder by a comma, for example: '-i "\\myserver1.domain.com\c$\tomcat\logs,\\myserver2.domain.com\c$\tomcat\logs"'
6. Newer System Log Parser builds only support System.Net.SecurityProtocolType of Tls11 and Tls12
7. For backward compatibility with older deployments, support for TLS 1.0 was readded; this had been automatically removed with the 0.10.x.x branches migration to .NET Framework 4.8; although System Log Parser supports connecting to deployments that are running older security protocols such as TLS 1.0 or TLS 1.1, it is *highly* recommended to use TLS 1.2 instead

Build 0.10.2.0 (Prerelease)
1. Added the ability of a Tomcat query to read server logs even if they are in use (by ArcGIS Server); in the case of reading logs that are in use, the data can be read by System Log Parser as soon as it has been flushed to the disk by ArcGIS Server
2. Added internal optimization with ArcGIS Server (web) queries by adjusting the Start time and End time ordering
3. Added additional application debug logging for several query meta data elements and adjusted the details of several existing logging events

Build 0.10.1.0 (Prerelease)
1. Added additional application debug logging for ArcGIS Server (web) log queries; the application debug logging can only be utilized when using slp.exe (the command-line version) and passing in the "-apploglevel INFO" or "-apploglevel DEBUG" command-line option; the default log level is OFF
2. Added the ability of an ArcGIS Server (FS) query to read service logs even if they are in use (by ArcGIS Server); in the case of reading logs that are in use, the data can be read by System Log Parser as soon as it has been flushed to the disk by ArcGIS Server
3. Added the ability of an ArcGIS Server (FS) query to read server logs even if they are in use (by ArcGIS Server); in the case of reading logs that are in use, the data can be read by System Log Parser as soon as it has been flushed to the disk by ArcGIS Server
4. Fixed issue where some error messages upon startup of System Log Parser were silently discarded
5. Added the ability to pass in a value to specify the folder where the application debug log is written; the default location is "C:\Users\[USERNAME]\Documents\System Log Parser\Logs"; this can now be overridden with the already existing "-downloadlocation" command-line option; so '-downloadlocation "D:\some\folder\with\write\access\"' would save all logs to D:\some\folder\with\write\access\
6. Added logic to skip any instance creation time log entries where the elapsed time is 0; although it is not anticipate to exist, adding in zeros would throw off the "accuracy" of the statistical representation of this data 
7. Clarified the description on the "Wait Time" and "Instance Creation Time" worksheets that the statistical representation does not include entries where the value was 0 (e.g. 0 seconds)
8. Changed the page title of the "Instance Creation Time" worksheet from "Instance Creation Statistics" to "Instance Creation Time Statistics"
9. Changed the tab title of "Wait Time" worksheet from "Wait Time" to "Wait Time (Queue Time)"
10. For a better user experience, the System Requirements for RAM was increased from 4GB to 8GB
11. Added the ability of an IIS query to read the logs even if they are in use (by IIS); in the case of reading logs that are in use, the data can be read by System Log Parser as soon as it has been flushed to the disk by IIS
12. Added additional application debug logging for ArcGIS Server (file system) log queries 

Build 0.10.0.0 (Prerelease)
1. Added enhanced statistics to the generated reports from System Log Parser; enhanced stats included additional information between the 95th and Max percentiles
2. Added some application debug logging for Azure
3. Fixed issue where System Log Parser would not read in any wait time and instance creation time log entries with an ArcGIS Server file system query
4. Added some application debug logging for the "Datasource Information" and "Datasource Analysis" worksheets (ArcGIS Server web queries)
5. Updated the System Log Parser URL in About System Log Parser to point back to the original System Log Parser "home page": https://www.arcgis.com/home/item.html?id=90134fb0f1c148a48c65319287dde2f7
6. Moved System Log Parser to .NET 4.8 Framework
7. Updated AWS libraries; System Log Parser now supports the following AWS regions:
   SLP Input		Name									Summary
   useast1			Amazon.RegionEndpoint.USEast1			The US East (Virginia) endpoint
   useast2			Amazon.RegionEndpoint.USEast2			The US East (Ohio) endpoint
   uswest1			Amazon.RegionEndpoint.USWest1			The US West (N. California) endpoint
   uswest2			Amazon.RegionEndpoint.USWest2			The US West (Oregon) endpoint
   eunorth1			Amazon.RegionEndpoint.EUNorth1			The EU North (Stockholm) endpoint
   euwest1			Amazon.RegionEndpoint.EUWest1			The EU West (Ireland) endpoint
   euwest2			Amazon.RegionEndpoint.EUWest2			The EU West (London) endpoint
   euwest3			Amazon.RegionEndpoint.EUWest3			The EU West (Paris) endpoint
   eucentral1		Amazon.RegionEndpoint.EUCentral1		The EU Central (Frankfurt) endpoint
   apeast1			Amazon.RegionEndpoint.APEast1			The Asia Pacific (Hong Kong) endpoint
   apnortheast1		Amazon.RegionEndpoint.APNortheast1		The Asia Pacific (Tokyo) endpoint
   apnortheast2		Amazon.RegionEndpoint.APNortheast2		The Asia Pacific (Seoul) endpoint
   apnortheast3		Amazon.RegionEndpoint.APNortheast3		The Asia Pacific (Osaka-Local) endpoint
   apsouth1			Amazon.RegionEndpoint.APSouth1			The Asia Pacific (Mumbai) endpoint
   apsoutheast1		Amazon.RegionEndpoint.APSoutheast1		The Asia Pacific (Singapore) endpoint
   apsoutheast2		Amazon.RegionEndpoint.APSoutheast2		The Asia Pacific (Sydney) endpoint
   saeast1			Amazon.RegionEndpoint.SAEast1			The South America (Sao Paulo) endpoint
   usgovcloudeast1	Amazon.RegionEndpoint.USGovCloudEast1	The US GovCloud East (Virginia) endpoint
   usgovcloudwest1	Amazon.RegionEndpoint.USGovCloudWest1	The US GovCloud West (Oregon) endpoint
   cnnorth1			Amazon.RegionEndpoint.CNNorth1			The China (Beijing) endpoint
   cnnorthwest1		Amazon.RegionEndpoint.CNNorthWest1		The China (Ningxia) endpoint
   cacentral1		Amazon.RegionEndpoint.CACentral1		The Canada (Central) endpoint
   mesouth1			Amazon.RegionEndpoint.MESouth1			The Middle East (Bahrain) endpoint
8. Updated EPPlus library
9. Updated Newtonsoft.Json library
10. Removed dependency of WindowsAzure.Storage library
11. Added support for Microsoft.Azure.Storage.Blob and Microsoft.Azure.Storage.Common libraries
12. Added support for Microsoft.Rest.ClientRuntime and Microsoft.Rest.ClientRuntime.Azure libraries
13. Updated Microsoft.Azure.KeyVault.Core library
14. Minor code clean-up
15. This version (0.10.x.x) will be last System Log Parser release to support log query uploads into ArcGIS Monitor 10.7.x/10.8.x

Build 0.9.6.0 (Prerelease)
1. Fixed some additional issues with the ArcGIS Server file system log queries where an Analysis Type of "ErrorsOnly" could not parse certain entries
2. Fixed an issue with ArcGIS Server file system log queries where under certain conditions an "ErrorsOnly" Analysis Type report could not be created with either a Text file or Spreadsheet file output
3. For AWS environments, added support and command line help documentation for the "-printfolders" boolean option
4. Fixed an issue where some error messages where silenced when run from the GUI
5. For ArcGIS Server web log queries, the "Add Service Details to Report" option has been slightly optimized to issue less requests
6. Added P95 and P99 (95th and 99th percentile statistics) to the "Throughput per Minute" worksheet table for reports with an Analysis Type of "Complete"
7. Enhanced the table header descriptions for the "Throughput per Minute" worksheet table
8. Added a notification warning if no log entries were found for a report with an Analysis Type of "ErrorsOnly"
9. For IIS log queries, support has been added for the X-Forwarded-For field to use in place of the c-ip field for the Client IP value; If the X-Forwarded-For field is not present or only contains an empty value, the "origial" c-ip field will be used instead
10. Fixed an issue with ArcGIS Server file system log queries where the elapsed time of some entries where numerically presented based on the locale of the machine running System Log Parser; from the file system, all ArcGIS Server elapsed time entries are consumed and analyzed in a consistent manner
11. For ArcGIS Server file system log queries from the GUI, the maximum Start Time has been increased from 90day(s) to 120day(s)
12.	Added an option to toggle the inclusion of the "Statistics By User" worksheet for ArcGUS Server Web, ArcGIS Server file system and IIS log queries (by default this is now false) 
13. Added a command line switch (e.g. the -sbu option) to toggle the inclusion of the "Statistics By User" worksheet (by default this is now false) 
14. From the System Log Parser GUI, the name "Output Folder" has been changed to "Report Folder" for all log queries
15.	Corrected a minor tab ordering issue in the System Log Parser GUI

Build 0.9.5.0 (Prerelease)
1. Fixed an issue with ArcGIS Server file system log queries where certain entries could not parsed
2. Fixed an issue with the ArcGIS Server (web and file system) log query where an Analysis Type of "ErrorsOnly" could crash System Log Parser when attempting to generate the report
3. Added support to the "Site Details" worksheet for SceneServer and WorkspaceServer service types 
4. Fixed an issue that prevented the System Log Parser GUI interface from allowing the ability to select an Analysis Type ErrorsOnly report with a Text file output for ArcGIS Server web and ArcGIS Server file system log queries
5. For ArcGIS Server log query reports with an Analysis Type of "WithOverviewCharts" or "Complete", the "Queue Time" worksheet has been renamed to "Wait Time" to better match the naming convention of ArcGIS Server
6. For ArcGIS Server log query reports that upload to ArcGIS Monitor the Counter Instances of "Tr/Interval Service Queueing" and "Tr/Interval Service Queueing Histogram (%)" have been changed to "Tr/Interval Service Wait Time" and "Tr/Interval Service Wait Time Histogram (%)", respectively; their associated Counter Names have also been adjusted to reflect this change

Build 0.9.4.0 (Prerelease)
1. Added some memory clean enhancements to SLP to help improve resource consumption after repeated GUI runs
2. Added ELBFS support to the interval SetSourceTypeFolder method
3. Enhanced the LogPrefix logic to automatically append "/AWSLogs" if this was omitted
4. Altered ELB log query logic by removing the requirement of the AWS ListBuckets method
5. Added command line help documentation for the "-listbuckets" boolean option
6. Separated the logic for the listbuckets routine. This is no longer part of the log query for a specific bucket.
7. Added a command line option boolean switch called "-listaccountid" (default is false) to list the AWS account id associated with the given awsAccessKeyId, awsSecretAccessKey and RegionEndpoint
8. Added command line help documentation for the "-listaccountid" boolean option
9. Expanded the supported security protocols for ELB/ALB log queries to include TLS 1.1 and TLS 1.2
10. Expanded the supported security protocols for CFRONT (CloudFront) log queries to include TLS 1.1 and TLS 1.2
11. Expanded the supported security protocols for Azure log queries to include TLS 1.1 and TLS 1.2
12. Added an "Instance Creation Time" worksheet to ArcGIS Server log query reports with an Analysis Type of "WithOverviewCharts" or "Complete". The "Instance Creation Time" worksheet list the times required for an service to start up if a request was made and an instance was not available (and the maximum number of concurrent instance was not yet reached).
13. Corrected an issue where some POST requests for ArcGIS Server log queries may not get counted in the statistical summaries
14. Removed the ClientIPs worksheet from ArcGIS Server log query reports with an Analysis Type of "WithOverviewCharts" or "Complete"
15. Added the Users worksheet in addition to the ClientIPs worksheet to IIS log query reports with an Analysis Type of "WithOverviewCharts" or "Complete"
16. Fixed an issue where Windows Authentication could not be used for some ArcGIS Server log queries
17. For a report generated from all log queries, the "Statistics" worksheet has been renamed to "Statistics By Resource" and an additional worksheet named "Statistics By User" has been added (For ArcGIS and IIS log queries) which lists resources with respect to the user who requested them
18. Improved the accuracy of the service type auto detection of Hosted, Dedicated and Shared services for the "Site Details" worksheet (for ArcGIS Server Web based log queries)
19. Added an ArcGIS Server capability count table to the Summary worksheet
20. Bring the Summary content of both the Text and Spreadsheet output closer together
21. Reduced the number of returned ArcGIS Server log entries chunks per web query from 9999 to 1000 to help improve accuracy and consistency
22. Added the "Domain" and "Server Machine" columns to the "Elapsed Time - All Resources" worksheet
23. Expanded the supported security protocols for ArcGIS Monitor log uploads to include TLS 1.1 and TLS 1.2

Build 0.9.3.0 (Prerelease)
1. Added support to run ELB log queries against gz compressed log files residing on the local disk through the -f ELBFS command line switch
2. Added support to run ELB log queries against plaintext log files residing on the local disk through the -f ELBFS command line switch
3. Expanded the command line help to include information on the "esr" switch; the "esr" switch toggles the "IsEnhancedSiteReport" option; In the GUI, this boolean option is presented as "Add Service Details to Report"
4. Added support for manually setting the ArcGIS Server Token Expiration and/or Request Timeout value from the command line
5. Expanded the command line help to include information on manually setting the an ArcGIS Server Token Expiration or Request Timeout value
6. The Vector Tile request signature categorization for ArcGIS Monitor has been changed from "vectortileserver" to "vectortileserver/tile"
7. Expanded verbosity of error details if a specific log file or log line cannot be read from an elb or alb source 
8. Improved the robustness of reading elb and alb logs originating from HTTP/2 gzip sources
9. Expanded verbosity of error details if a specific log file or log line cannot be read from an iis source
10. Improved the robustness of detecting the required iis w3c headers that could be missing or incomplete
11. Removed iis log source restriction: the specified target directory no longer needs to contain "w3svc" or "inetpub"
12. Expanded verbosity of error details if a specific log file or log line cannot be read from an azure source
13. Expanded verbosity of error details if a specific log file or log line cannot be read from a tomcat source
14. Expanded verbosity of error details if a specific log file or log line cannot be read from a cloudfront source
15. Expanded verbosity of error details if a specific log file or log line cannot be read from an arcgis server web source
16. Expanded verbosity of error details if a specific log file or log line cannot be read from an arcgis server file system source
17. Fixed several issues with the "Throughput per Minute" worksheet which could cause the report generation to fail 
18. Changed the default ArcGIS Server URL from "https://gisserver.domain.com:6443/arcgis" to "https://gisserver.domain.com/server"

Build 0.9.2.0 (Prerelease)
1. For log query uploads to ArcGIS Monitor, a "Response Time per Service Type (Sec)" counter has been added

Build 0.9.1.0 (Prerelease)
1. Further enhanced the resource id/GUID name consolidation to support additional raster type requests
2. Fixed an issue with ELB and ALB log queries where a "bad" log entry could stop the progress of the read
3. In addition to working with the existing Azure CloudBlockBlob storage, SLP now supports the newer CloudAppendBlob storage format (for Azure log queries)
4. Due to the CloudAppendBlob support, SLP is also now compatible with the newer JSON Lines log format (for Azure log queries)
5. Added several checks to help avoid a potential "division by zero" error for reports with an Analysis Type of "WithOverviewCharts" or "Complete"
6. Fixed issue with some log queries where certain services would incorrectly be marked as a "Hosted service" if the web adaptor instances of the site was called "hosted"

Build 0.9.0.0 (Prerelease)
1. Fixed issue where "Client IP" column in (from a Complete Analysis report) may not be listed with a CloudFront log query in the "Elapsed Time of All Resources" worksheet
2. Fixed issue where the "Users" worksheet (from a Complete Analysis report) may be listed instead of the the "ClientIPs" worksheet with a CloudFront log query
3. With a Complete Analysis report, the "ArcGIS Log File" column was changed to "Log Source"
4. With a Complete Analysis report, the "Elapsed Time of All Resources" worksheet has been renamed to "Elapsed Time - All Resources"
5. Fixed some of the  ELB and CloudFront tooltips which did not provide the correct information
6. Added the "-help" option in addition to the "-h" option for displaying "help" from the command line (e.g. with slp.exe)
7. Added ability to read Azure logs and perform queries
8. Added timespan details in the generated report for both the query time range and log data time range
9. Improved log datetime filtering accuracy for certain sources where the some files may contain a few enteries of the previous hour
10. Changed the maximum allowable lines of generated log data (per worksheet) in the spreadsheet report to be 1,000,000
11. Added the ability of SLP to automatically create a text file of the data for a worksheet (e.g. "Throughput per Minute", Elapsed Time - All Resources) that exceeds the maximum allowable lines
12. Added some report generation progress feedback to the SLP GUI
13. Added a check in the SLP GUI to help ensure that only the Analysis Type of "Simple" can be used with a Report Type of "TextFile"
14. Increased the logs detail of information for traditional Feature Server requests from a VERBOSE report 
15. For ArcGIS Monitor log uploads, items like tiles and service definition requests are now automatically saved to the repository
16. Optimized the VerboseMode and ErrorsOnly Report column formatting to improve creation times
17. System Log Parser now consolidates jobid GUIDs within specific ArcGIS-type requests in order to help make the generated statistics easier to read. The exception to this are requests to ArcGIS Portal resources (e.g. "/sharing/rest/content/items/[guid]")...these are left in their original form.
18. Added ALB/ELB fixes for malformed requests
19. Added improvements to multistream gzip decompression for incomplete files
20. Added a fix to ArcGISFS log queries to improve accuracy of read based on certain entries
21. Added a fix to ArcGISFS log queries for an Analysis Type of ErrorsOnly...previous builds would not find any WARNING or SEVERE log entries, under this condition
22. Fixed an issue when creating the Statistics worksheet where it could take a long time if the log query resulted in many different resources
23. Added a "Response|Request Sizes" worksheet for reports of Analysis Type "WithOverviewCharts and "Complete" which show the top resources for the largest response and request sizes

Build 0.8.19.0 (Prerelease)
1. Adjusted the queueing counts in the ArcGIS Server report to not include entries with an elapsed time of 0. With this adjustment the count now reflect requests that queued (instead of any request).
2. Added "Service Requests" count column to the "Queue Time" worksheet to given an improved perspective of the impact of the queue time entries
3. Fixed issue with the SiteDetail worksheet where some services would not be listed if no extensions were enabled
4. Added an "Is Enabled" column to the SiteDetail worksheet to help filter out extensions that are enabled or disabled
5. For ArcGIS Server (Web) log queries that are uploaded to ArcGIS Monitor, the following metrics have been added under "Tr/Interval Service Queueing":
   TotalSecondsQueued
   TotalRequestsQueued
   TotalServicesQueued   
   Tr/Interval Service Queueing Histogram (%)
6. For IIS log queries that are uploaded to ArcGIS Monitor, the domain and username information is reported on
   IIS logs will contains this information if the "User Name (cs-username)" is enabled (in IIS) and the ArcGIS site's Web Adaptor is configured for Windows Authentication and authenticated users made requests during the collection interval
7. Fixed issue with ArcGIS Server (Web) log queries uploaded to ArcGIS Monitor where the values of the "Tr/Interval Response Time Histogram (%)" counters were the counts instead of the percentage of counts
8. Added ability to read Tomcat access logs and perform queries (command line only). To enable Tomcat access logs (Note: with this setting, the logs will rotate every hour):
   Find the server.xml file within the appropriate Tomcat installation
   Make backup copy of original server.xml file
   Open server.xml in text editor
   Replace the following line:
	<!--    
    <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" prefix="localhost_access_log." suffix=".txt" pattern="common" resolveHosts="false"/>

-->
   With the following line:
    	<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" fileDateFormat="yyyy-MM-dd.HH" pattern="%h %l %u %t &quot;%r&quot; %s %b %v %p %D" prefix="localhost_access_log." resolveHosts="false" suffix=".txt"/>
   Save edits
   Restart Tomcat or associated product service
   Note: in this example, the suffix is set to ".txt" but using ".log" will also work with slp.exe
9. Fixed an issue with ArcGIS Server File System log parsing when a "partial" log is encountered. A "partial" log would have only one line and typically resemble the following:
   <?xml version="1.0" encoding="utf-8" ?>
10. Fixed an issue with ArcGIS Server (web) log queries when the "Add Service Details to Report" option was enabled and the operation was Cancelled. 
    If System Log Parser was in the middle of collecting the service manifest information, the process would continue until all services were read.
    This background process now stops much more quickly.
11. For ArcGIS Server (web) log queries, there is now the option to manually provide an ArcGIS Server or ArcGIS Portal token, instead Windows Authentication or passing in a username/
.
    Examples of generating a token to use with System Log Parser:
     To generate an ArcGIS Server token...
        For a Server URL such as: https://[HOSTNAME]:6443/arcgis
        Connect to the ArcGIS Server Generate Token resource: https://[HOSTNAME]:6443/arcgis/admin/generateToken
        Enter in the username and password for the PSA account, use "Request IP" for Client
        Copy the generated token to use with System Log Parser
     To generate a Portal Server token (with a Portal Federation Login)...
        For a Server URL such as: https://[HOSTNAME]/arcgis
        Connect to the ArcGIS Adminstrator Directory login resource: https://[HOSTNAME]/arcgis/admin/login   
	Copy the listed 'Webapp URL' from the Portal Federation Login section
        Connect to the ArcGIS Portal Generate Token resource: https://[HOSTNAME]/arcgis/sharing/generateToken   (assuming resource is accessible)
        Enter in the username and password for the appropriate account, select 'Webapp URL' for Client and provide the 'Webapp URL' from the previous resource
        Copy the generated token to use with System Log Parser
12. Minor formatting adjustments and column comment corrections for spreadsheet generated reports
13. Fixed an issue where if the "Add Service Details to Report" option was selected, System Log Parser would not read the logs and return a warning of "Could not collect logs. Exception: Object reference not set to an instance of an object"
14. Improved the clarity of the warning message for ArcGIS Server (web) log queries, if the supplied Server URL was invalid or could not be utilized

Build 0.8.18.0 (Prerelease)
1. Included the Web Server Certificate Alias field in the Site Details worksheet
2. Added support for several ArcGIS Server 10.6.1 features:
   Expanded the Site Details worksheet to include hardware information on each machine in the Site
   Added a worksheet called Queue Time which statistically breaks down the wait time collected from each service	
3. Fixes for gzip decompression of the multistream ALB logs (as well as CloudFront logs)
4. Changes for (ELB/IIS/CloudFront) log collection uploads into ArcGIS Monitor:   
   The Counter name for the Instance "Network Sent MB/Interval" has been changed from "TotalMegabytes" to "TotalMegabytesSent"
   The Instance "Network Received MB/Interval" has been added with Counter name "TotalMegabytesReceived"
5. If a ReportType of "DownloadLogsOnly" was selected and the log source is ELB or CloudFront the log names now have a suffix of ".txt"
6. If an AnalysisType of "Complete" was selected, the data column of "CloudFront Edge Result Type" in the "Elapsed Time of All Resources" worksheet will default to "-" for log source where this value does not apply
7. If an AnalysisType of "Complete" was selected against an ALB log source, the "Elapsed Time of All Resources" worksheet will populate the "TargetGroup" column...otherwise this value will default to "-"
8. Added statistics on the resource request total for spreadsheet or text file generated reports
9. Provided a notification on the "Statistics" section of a spreadsheet or text file generated report if no resource requests were found for the given period of time
10. Increased the precision accuracy of the Count Pct and Sum Pct columns in the "Statistics" worksheet of the Spreadsheet report
11. Changes for ArcGIS (Web/File System) log collection uploads into ArcGIS Monitor:   
    The Counter name for "Users Tr/Sample" has been changed to "Users Tr/Interval Total"
    The Counter name for "TotalGBSent Tr/Sample" has been changed to "TotalMBSent Tr/Interval Total"
    The Counter name for "TotalRequests Type" has been changed to "TotalRequests Tr/Interval Total"
    The Counter "RequestAverage Type" has been added
    The Counter "< 3 sec Tr/Interval Response Time Histogram (%)" has been added
    The Counter ">= 10 and < 20 sec Tr/Interval Response Time Histogram (%)" has been added
    The Counter ">= 20 and < 30 sec Tr/Interval Response Time Histogram (%)" has been added
    The Counter ">= 3 and < 10 sec Tr/Interval Response Time Histogram (%)" has been added
    The Counter ">= 30 and < 60 sec Tr/Interval Response Time Histogram (%)" has been added
    The Counter ">= 60 sec Tr/Interval Response Time Histogram (%)" has been added
12. If a Report Type of "DownloadLogsOnly" is selected for an ELB or CloudFront log query and the logs are stored compressed, the raw log (*.log.gz) and decompressed log (*.log.txt) will be saved locally

Build 0.8.17.0 (Prerelease)
1. Remove background spreadsheet grid lines from the Statistics worksheet
2. Expanded the Datasource Details worksheet
   This has been broken up into two worksheets:
   Datasource Information (formally known as Datasource Details) -- which lists all observable services and their respective datasource information
   Datasource Analysis -- which lists datasets by their occurence in services as well as map documents by their occurence in services
3. Added wide character support for ArcGIS Monitor

Build 0.8.16.0 (Prerelease)
1. Initial support for CloudFront log parsing (command-line and GUI)
2. Added new Report Type, "DownloadLogsOnly". This report only downloads the logs available from the remote source from the queried time window as saved them to the specified location.
3. Added command-line switch "-downloadlocation" to specify custom location to save downloaded logs
4. Added GUI support for the new Report Type, "DownloadLogsOnly"
5. Added checks to validate that the Token Service URL is defined when querying the /rest/info resource page. In some deployments, this may not be set for certain access points to the installation.
6. Added a "Datasource Details" worksheet to the "Add Service Details to Report" option. This worksheet lists information on the backend datasources for each service, if available.
7. Expanded the "Site Detail" worksheet to include information on enabled extensions for each service. The capabilities of each extension are also listed.
8. Added code "100002" to the built-in ArcGIS Server log parser query filter to include GPServer.ExecuteJob.[ServiceName] Method times for geoprocessing services. This log entry reflects the total time taken by geoprocessing service to fullfil a job request.
9. Fixed issue in the report where the ELB name would appear empty, although there are conditions where this is valid, the blank andn empty string has been replaced with "[empty]" 
10. For ELB log query uploads to ArcGIS Monitor the Validation counter called "TotalELBNames" has been renamed to "TotalNames"
11. For generated reports from ELB logs the "ELB Name (Total)" field has been renamed to "Names (Total)"
12. Minor updates to the command-line help
13. Fixed issue where System Log Parser would crash if the number of lines within a spreadsheet's worksheet exceeded 1,048,576
14. Fixed issue where System Log Parser could not retrieve the ArcGIS Server Site Details and generate a report if a service did not have a cluster set (e.g. "default") in its configuration
15. The System Log Parser extension folder now includes an "elb.exe.config" file to accompany the elb.exe executable

Build 0.8.15.1 (Prerelease)
1. Updated build number

Build 0.8.15.0 (Prerelease)
1. For ELB/IIS log query uploads to ArcGIS Monitor, the counterCategory for items containing "/arcgis/directories/" have been changed from OTHER to REST
2. For ELB/IIS log query uploads to ArcGIS Monitor, generic REST and SOAP requests (e.g. non-specific ArcGIS capability requests) are now always uploaded. Previous builts uploaded these items if the "-uploadstatic" option was true.
3. Fixed issue where the "-uploadother" was not true by default. With this fix, all non-ArcGIS requests (that are not considered static requests like *.html, *.js, *.png, etc...) will be uploaded to ArcGIS Monitor.
4. Fixed issue where System Log Parser would crash creating an Excel report if the line entry in the queried ELB log was partial and not complete
5. When a line entry for a queried ELB log is found to be partial and not complete, System Log Parser will identify the item with an "[incomplete log entry]" designation for its resource
6. When a line entry for a queried ELB log is found to be incomplete, System Log Parser will attempt to read as Datetime, Status Code or Elapsed Time, if available
7. For queried ELB log entries, System Log Parser by default will assume an HTTP Status code of 500 instead of 0 (the previous default)  
8. For queried ELB log entries, System Log Parser by default will initialize the datetime to Epoch
9. Fixed issue where System Log Parser could incorrectly identify a resource's ArcGIS Capability
10. The following labels (e.g. counter instances) have either been renamed or how they report the information has been slightly altered:
    HTTP 400 Codes/Interval --> HTTP 400 tr/Interval
    HTTP Error/Interval --> HTTP 500 tr/Interval
    HTTP OK/Interval --> HTTP 200 tr/Interval (and "HTTP 300 tr/Interval")
11. The following counter names have been moved:
    HTTP400s --> from HTTP Error/Interval to HTTP 400 tr/Interval
12. The following counter names have been removed from the HTTP Error/Interval label
    FailedRequest (%)
    FailedRequests 
13. The following label has been created 
    "HTTP Code (%)"
14. The following counter names have been moved:
    Http 500 (%) --> from HTTP Error/Interval to HTTP Code (%)
15. The following counters have been added: 
    Http 200 (%)
    Http 300 (%)
    Http 400 (%)

Build 0.8.14.0 (Prerelease)
1. The following labels (e.g. counter instances) have either been renamed or how they report the information has been slightly altered:
   GB Sample Sent --> Network Sent MB/Interval
   HTTP 400 Codes/Sample --> HTTP 400 Codes/Interval
   HTTP Error/Sample --> HTTP Error/Interval
   HTTP OK/Sample --> HTTP OK/Interval
   IPs/Sample --> IPs/Interval
   Response Time (Seconds) --> Response Time (Sec)
   Tr/Minute Peak --> Tr/Min Peak
   Tr/Sample ArcGIS Endpoint Definition --> Tr/Interval ArcGIS Endpoint Definition
   Tr/Sample ArcGIS Server --> Tr/Interval ArcGIS Server
   Tr/Sample ArcGIS Server Extension --> Tr/Interval ArcGIS Server Extension
   Tr/Sample Non-ArcGIS --> Tr/Interval Non-ArcGIS
   Tr/Sample OGC --> Tr/Interval OGC
   Tr/Sample Portal --> Tr/Interval Portal
   Tr/Sample Response Time Histogram --> Tr/Interval Response Time Histogram
   Tr/Sample Tile --> Tr/Interval Tile
   Tr/Sample Total --> Tr/Interval Total
2. The following counter names have been renamed:
   TotalGigabytes --> TotalMegabytes
   FailedRequest% --> FailedRequest (%)
3. The following counters have been added: 
   Http 500 (%)
4. For uploads into ArcGIS Monitor, a fix was added to ensure the counterCategory type is properly set for either an extension or task collection

Build 0.8.13.0 (Prerelease)
1. Added support for ELB log query uploads (into ArcGIS Monitor) to be run as an extension (every 5min or 15min, in addition to a task which is 1hr). By design, the log rotation mechanism of IIS mechanism only supports a resolution up to 1hr.
2. In addition to the "HTTP400s (Tr/hour)" counter total for ELB and IIS log queries, the HTTP 400 codes have been broken up further into a dedicated group called "HTTP 400 Codes/Hour". This includes the following HTTP 400 codes: 400, 401, 403, 408, 498, 499 and 4xx (all other 400 codes).
3. Fixed issue where ArcGIS (Web) log queries (into ArcGIS Monitor) may not properly count WorkflowManagerServer and SteamServer requests
4. Added additional columns to the Excel Statistics worksheet to assist with filtering. The Capability column was added for ArcGIS log query reports. The Instance and Capability column was added for ELB and IIS log query reports.
5. Added a Failed Request Percentage counter to ELB and IIS uploads (into ArcGIS Monitor). This counter will appear under the "HTTP Error/Hour" instance.
6. Added Failed Request Total counter to ELB and IIS uploads (into ArcGIS Monitor). This counter will appear under the "HTTP Error/Hour" instance.
7. Fixed issue where some failed requests (from ELB log queries) were not reported as HTTP 500 Errors
8. In order to provide more clarity on the "Server" counter totals for ELB and IIS log queries (found under the instance names of "Tr/Hour ArcGIS Server" and "Tr/Hour ArcGIS Server" and "Tr/Hour ArcGIS Server Extension") an additional instance called "Tr/Hour ArcGIS Endpoint Definition" has been created. These totals count hits to ArcGIS services that do NOT contain function calls like (export, query or find). 
9. Added the version number to the output of the command-line Help (slp.exe -h)
10. Added some missing choices for several of the command-line parameter options
11. The labels for all (hour based) log query counters uploaded to ArcGIS Monitor have been renamed to from "Tr/Hour" to "Tr/Sample"
12. Added SampleInterval (seconds) as a Validation counter for ELB/IIS log query uploads (into ArcGIS Monitor)

Build 0.8.12.0 (Prerelease)
1. Enabled ArcGIS Server (File System) to create a Report with an Analysis Type of VerboseMode
2. Minor formatting changes on the Elapsed Time of All Resources worksheet for a Complete Analysis Type Report
3. Added .NET Regular Expression support to slp.exe for all log queries. Note: this feature is for Advanced Use Only!
   	a. Use the Regular Expression Pattern (-regexpattern) to pass in a string containing the regex rule (the default is an empty pattern...which is to match everything)
   	b. Use the Regular Expression IgnoreCase Boolean (-regexignorecase) to toggle case-sensitivity (the default is true...which is to the ignore case)
   For ELB, the regular expression pattern will match against the URL field
   For IIS, the regular expression pattern will match against the uri-stem field
   For ArcGIS Server, the regular expression pattern will match against the source field
   For a quick reference on the Regular Expression Language in .NET see the following online resource: https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference
4. Added .NET Regular Expression support to System Log Parser GUI for all log queries
5. Added the ability for slp.exe to toggle the ability of uploading "Other" (-uploadother) non-ArcGIS Server requests into ArcGIS Monitor (default is true...which is to upload)
6. Fixed issue with IIS log query where the Summary worksheet in the report, under some circumstances, was not able obtain Source Server (IIS IP Address) from the logs
7. Fixed issue with System Log Parser GUI where the Analysis Type of ErrorsOnly would show up as an option from the drop down list for ELB and IIS log queries
8. Minor formatting changes to the System Log Parser GUI 

Build 0.8.11.0 (Prerelease)
1. Fixed a data formatting display issue in the Site Details worksheet
2. For ArcGIS Server WorkflowManager log query uploads to ArcGIS Monitor, the counter name has been changed from WorkflowManagerServerRequests to WorkflowManagerServer
3. Added StreamServer (e.g. GeoEvent Server) support to the Site Details worksheet
4. Added StreamServer (e.g. GeoEvent Server) support to log data uploaded into ArcGIS Monitor
5. For improved group and analysis, there are Counter changes for ELB and IIS log query uploads to ArcGIS Monitor:
	a. The "Tr/hour" instance has been added to hold all counters related to throughput
	b. All counters in the "ArcGIS Server", "ArcGIS Server Extension", "OGC", "Other" and "Tiles" instances have been moved to the "Tr/hour" instance
	c. Moved AvgRequestResponseTime from "Requests" Instance to "Response Time (second)" Instance
	d. Moved TotalRequests (Tr/hour) from "Requests" Instance to "Tr/minute" Instance
	e. Moved HTTP200s (Tr/hour) from "Code" Instance to "HTTP OK/hour" Instance
	f. Moved HTTP300s (Tr/hour) from "Code" Instance to "HTTP OK/hour" Instance
	g. Moved HTTP400s (Tr/hour) from "Code" Instance to "HTTP Errors/hour" Instance
	h. Moved HTTP500s (Tr/hour) from "Code" Instance to "HTTP Errors/hour" Instance
	i. The description of "(Tr/hour)" has been moved from all counter names to the respective parent folder
	j. TotalIPs (IPs/hour) has been renamed to TotalIPs; the parent folder has been renamed to IPs/hour
	k. Moved Tr/minute Statistics from "Requests" Instance to "Peak Tr/minute" Instance
 	l. The Tr/minute Max counter has been renamed to Max and moved to "Peak Tr/minute" Instance
 	m. The Tr/minute P95 counter has been renamed to P95 and moved to "Peak Tr/minute" Instance
	n. The Tr/minute TotalSamples counter has been renamed to TotalSamples and moved to "Peak Tr/minute" Instance
 	o. Removed the Tr/minute Avg counter
 	p. Removed the Tr/minute Min counter
	q. Removed the Tr/minute P5 counter 
	r. Removed the Tr/minute P25 counter 
 	s. Removed the Tr/minute P50 counter
	t. Removed the Tr/minute P75 counter
 	u. Removed the Tr/minute P99 counter	
	All data from previously collected counters, under the previous Instance names, will be lost

Build 0.8.10.0 (Prerelease)
1. System Log Parser now supports Portal Federation Logins

Build 0.8.9.0 (Prerelease)
1. Request details for "OtherRequests" are no longer uploaded by default for ArcGIS Monitor logEntry uploads.
   The ELB or IIS extension for ArcGIS Monitor will have to be configured to specifically enable the uploading of this information.
2. GUI input fields such as Server URL from ArcGIS Server (Web) or Bucket Name from ELB have been "trimmed" to remove the white-spaces and the end and beginning in order to prevent unintended "blank characters" from being passed in
3. Various, but minor changes to the command-line Help descriptions and GUI tooltips for some input options
4. Update the System Log Parser's Elapsed Time Minimum field in the GUI to reflect the same default value of the command-line option, -etminimum. This default value (for the command-line) was recently changed from 3 to 0.

Build 0.8.8.0 (Prerelease)
1. For the Site Details worksheet, Min Instances (Cluster) and Max Instances (Cluster) columns have been added to show the total number of configured instances of the service based on how many machines are participating in its respective cluster.
   This is in addition to the original columns of Min Instances (Node) and Max Instances (Node) which list the total number of configured instances with respect to each node (or machine).
2. For the Site Details worksheet, the name of the Cluster that each service is participating in has been added
3. For the Site Details worksheet, Max Startup Time for each service has been added
4. For the Site Details worksheet, the configured Capabilities of each service, if available, has been added
5. For the Site Details worksheet, the total number of published services (running or not) has been added to the bottom of the Service Name column
6. Changed the source type field in the report summary from AGS to ArcGISServer where ArcGIS Server (Web) was the log source type. This is also reflected in the file name of the report.
7. Changed the source type field in the report summary from AGSFS to ArcGISServerFS where ArcGIS Server (File System) was the log source type. This is also reflected in the file name of the report.

Build 0.8.7.1 (Prerelease)
1. Fixed a calculation of the Service Requests column on the Site Details worksheet where the number reported was not the correct representation of "the total number of requests for that service"

Build 0.8.7.0 (Prerelease)
1. Changed the default value for the Elapsed Time Minimum (-etminimum) from 3 to 0. This will include all requests by default in the Complete Report (All Resources Elapsed Times worksheet).
2. Add an Response Time Histogram grouping on the Summary worksheet to classify All requests (regardless of the passed in Elapsed Time Minimum value) based on their respective time (e.g. less than 3 seconds; equal to 3 seconds but less than 10, etc...)
3. Add an Response Time Histogram grouping to the ArcGIS Monitor upload for ELB and IIS log queries
4. Added a Throughput per Minute worksheet to the Complete report. The Throughput per Minute worksheet is a compliment to the Time worksheet chart and breakdown the throughput of all requests by the minute in tabular form
5. For non-ArcGIS Server log queries a "Path" column was added to assist with making spreadsheet filtering more convenient. This column is derived from the last part of URL Path.
6. Added *ALL* Report Types to the special time frame case of "End Time: 1hr (ago)  Start Time 2hr (ago)". In this case, the previous full hour time range is taken and all report types will now read and present the same information. In previous builds only a Report Type of ArcGIS Monitor followed this rule. 
7. Removed "Server Version (Build)" and "Server LogLevel (FileAge)" from ELB and IIS reports as such information is not applicable
8. In Addition to the "TotalLogsRead" Validation counter (ELB and IIS), an "TotalELBNames" Validation counter (ELB only) has been include to assist with QA
9. ELB queries will no longer create reports or upload data to ArcGIS Monitor if logs from multiple AWS Account Ids are discovered within the configured bucketname. Such a scenario will require additional input in order to filter out the "unwanted" logs. This was done for improved data integrity to ensure that the appropriate and expected logs are being analyzed.
10. Statistics are now performed on *ALL* requests (successful or not). Note: All elapsed times as reported from ArcGIS Server are successful. 
11. ELB and IIS ArcGIS Monitor uploads now include an Average Response Time per Request as well as a listing of Throughput per Minute statistics
12. ELB requests that have an incomplete log entry (e.g. "backend HTTP Status = 0" or "elapsed time = -1"), now have their HTTP Status taken from ELB and their elapsed time changed to 0
13. Added a check to prevent an ArcGIS Server (Web) log query from starting when the "Use Windows Authentication" connection was enabled but the Server URL was not point to a Web Adaptor deployment
14. Added a check to prevent the specified End Time from creating a DateTime younger than the DateTime created from the specified Start Time

Build 0.8.6.0 (Prerelease)
1. Enhanced the Complete Report (All Resources Elapsed Times worksheet) by adding the HTTP Status field

Build 0.8.5.3 (Prerelease)
1. Minor correction of the System Log Parser library versioning

Build 0.8.5.2 (Prerelease)
1. Fixed rendering issue where the password field for the ArcGIS Server (Web) window was not visible

Build 0.8.5.1 (Prerelease)
1. Fixed EndTime hour issue with Analysis Type "VerboseMode". With "VerboseMode", only an EndTime "Now" can be used.
2. Synchronized all dll and exe versions to the release number

Build 0.8.5.0 (Prerelease)
1. Added an Analysis Type called "VerboseMode" to ArcGIS Server (Web) log queries. If the ArcGIS Server instance contains VERBOSE log entries, this type will generate a special report that can breaks down each type of request with detailed information.

Build 0.8.4.0 (Prerelease)
1. Fixed issue where under certain circumstances, the Minimum statistical value for a ELB resource would get reported as -1
2. Fixed issue with the ELB log query where the optional "ELB Name Match" input would only be read in if the optional "Log Prefix" input was populated
3. Addd a Client IP chart detailing the most popular IPs based on the number of respective requests. This chart can be found for an ELB or IIS log search with an Analysis Type of WithOverviewCharts or Complete.
4. Enhanced the Complete Report (All Resources Elapsed Times worksheet) for an IIS log query by constructing the requested url
5. Added an ArcGIS Server User chart (Total Requests per User)
6. Fixed issue with the Complete Report (All Resources Elapsed Times worksheet) where the Content Length was zero for an ArcGIS Server FS (File System) log query
7. Clarified response time minimum to be Elapsed Time Minimum (-etminimum)
8. Fixed issue where some selected log queries did not honor the Elapsed time minimum if it was changed from the default value
9. Fixed issue with ArcGIS Server FS (File System) log query where the log file's datetime entry was read in and internally (and incorrectly) converted to UTC. The datetime entry of each line is in LocalTime.
10. Added a fix to workaround an ArcGIS Server FS (File System) datetime precision issue. The datetime entry of each line include milliseconds but stated precision can be ambiguous ('2017-07-20T16:50:01,72' is meant to be '2017-07-20T16:50:01,072' but on conversion is interpreted as '2017-07-20T16:50:01,720').
    This resulted in chance of some of the requests listed in the Complete Report (All Resources Elapsed Times worksheet) to be slightly out of order chronologically (for each unique minute listed).
11. For clarity, the Date Time column in the All Resources Elapsed Times worksheet (of the Complete Report) now includes milliseconds
12. Enhanced the Complete Report (All Resources Elapsed Times worksheet) to now include the same decimal precision (e.g. 5) found in the ArcGIS Server logs
13. Enhanced the Complete Report (All Resources Elapsed Times worksheet) to now include the name of the source log file where the request entry occurred. This column is empty for an ArcGIS Server (Web) log query as the API does not provide this information.
14. Enhanced the Complete Report (All Resources Elapsed Times worksheet) to now include the ArcGIS Server log entry Code and Type for ArcGIS Server (Web and File System) log queries
15. Log entries of Type 'INFO' and code '10138' were listed as a request in the statistics table and as a request in the Complete Report (All Resources Elapsed Times worksheet). These have now been removed and are no longer included in the report.

Build 0.8.3.0 (Prerelease)
1. Reset the default output directory to be based on "[Username's Documents Folder]\System Log Parser\Reports" instead of "[Username's Documents Folder]\Documents"
2. Fixed bug with IIS uploads into ArcGIS Monitor where the collection would run at the top of the hour but IIS had not yet rotated its logs (from the previous hour). SLP now intentionally waits for several minutes until IIS has rotated its logs.

Build 0.8.2.0 (Prerelease)
1. Added the ability to filter/search ELB logs based on the load balancer name for the case where multiple sites are writing ELB logs to the same folder
2. Enhanced the Complete Report to just display request details for response times greater than a configurable amount of seconds (default is 3). This is adjusted from the "Response Time Minimum" field in the GUI.
3. Greatly improved the generation performance of the Complete Report
4. "OtherRequests" are now uploaded for ELB and IIS ArcGIS Monitor logEntry uploads
5. "OtherRequests" are now uploaded with Source as UriStemResource instead of Asset
6. logEntry upload now contain the requestURL, if it was available in the log (e.g. ELB)
7. The Complete Report now contains the requestURL, if it was available in the log (e.g. ELB)
8. The ArcGIS Server (Web) log parsing GUI section now disables the "Add Service Details to Report" option if an Analysis Type of "ErrorsOnly" is selected
9. Fixed issue with ArcGIS Server FS (File System) and IIS where the log query would stop with "Sequence contained no elements" if a log was encountered that had file size of 0 (zero)

Build 0.8.1.2 (Prerelease)
1. When using ArcGIS Server FS (File System) log parsing, the time ranges in the GUI have been increased to match ArcGIS Server (File System)
2. Internal code clean-up; removed unused libraries from core SLP logic
3. The Third_Party_Software_README.txt has been updated to include information on all the third party support libraries used by System Log Parser

Build 0.8.1.1 (Prerelease)
1. Fixed problem in the GUI where the Elastic Load Balancing (ELB) log parsing Secret Key field was disabled and unable to accept input text

Build 0.8.1.0 (Prerelease)
1. Added timestamps to the report listing the date range (oldest entry and newest entry) of the data discovered during the query
2. Added Site Details output if the "Add Service Details to Report" option was selected for a Report Type of TextFile
3. Corrected the Title of TextFile Report to list "System Log Parser" at the top of the page instead of "Elastic Load Balancer"
4. Enhanced the readability of the TextFile report file name
5. When using ArcGIS Server FS (File System) log parsing, requests to the root page of a service (e.g. '/') now show up as "/" under Method; In the previous version the Method was empty.
6. When using ArcGIS Server FS (File System) log parsing, the maximum time ranges in the GUI are now represented in days instead of weeks
7. Fixed the ArcGIS Server (Web) log parsing GUI where the Analyze button was still disabled if the "Use Windows Authentication" button was selected even when the Server Url and Output Directory fields were populated

Build 0.8.0.0 (Prerelease)
1. A redesigned GUI (SystemLogsGUI.exe) has now been added to support the SLP log query functions of: ArcGIS Server (via the web), ArcGIS Server (via the file system), Elastic Load Balancing, Internet Information Services (via the file system). 
   ArcGIS Monitor extensions and tasks should still refer to slp.exe in their respective configurations.

Build 0.7.4.0 (Prerelease)
1. Added support for the command line version of System Log Parser (slp.exe) to accept inputs from ArcGIS Monitor in non-plaintext format

Build 0.7.3.1 (Prerelease)
1. Corrected the count of Total Requests (IIS and ELB) where the total was not matching the sum of all HTTP 200, HTTP 300, HTTP 400 and HTTP 500 requests
2. Corrected console output counter totals (MapServer, ImageServer, SOAP, etc...) where some 4xx/5xx requests could be included in sums

Build 0.7.3.0 (Prerelease)
1. Changed webTrack uploads to utilize the same Epoch time value for gmtMinute and gmtHour. This was done to improve the report functionality in ArcGIS Monitor.
2. Changed webTrack uploads to utilize a counterType of 'slp-web-ip' instead of 'slp-iis-ip'. This was done to improve the report functionality in ArcGIS Monitor.
3. Removed WebTrackIndex and LogEntryIndex uploads. This is now done in ArcGIS Monitor.
4. Removed the console output totals for static resources (e.g. TXT, CSS, PNG, etc...). This was done to save on optimize performance and storage space.
5. Various internal changes on how error exceptions are handled

Build 0.7.2.0 (Prerelease)
1. Expanded the detection of an WMTS tile request for IIS/ELB
2. Added a count of the source being tracked in the new logentry index upload
3. Added ability to be detected by ArcGIS Monitor as being run as a task (ArcGIS Logs, ArcGIS Errors, IIS Logs, ELB Logs) or extension (ArcGIS Errors)

Build 0.7.1.1 (Prerelease)
1. Fixed case-sensitivity issue with uploads into logentry for the resource and method properties
2. Fixed issue with uploads into logentry where code was not reflecting the httpstatus code of the response

Build 0.7.1.0 (Prerelease)
1. Logentry and webtracks optimizations (index uploads)
2. Added floor function property to logentry uploads
3. Fixed lastmodified logfile datetime issue with IIS
4. Added optimizations for ArcGIS request uploads into logentry

Build 0.7.0.0 (Prerelease)
1. New SLP engine released

Build 0.6.3.1 (Prerelease)
1. Fixed an issue where some items involving a date time conversion might run into problems with international deployments. Where appropriate, SLP now utilizes the ISO 8601 standard when working with date and time-related data.
2. Fixed a minor issue in Site Details where the Max Record for a Globe Service would be blank...it should be "n/a"

Build 0.6.3.0 (Prerelease)
1. Corrected a small issue as well as expanded on the summarized log data that is uploaded to ArcGIS Monitor for IIS traffic

Build 0.6.2.0 (Prerelease)
--------------
1. The example URL has been changed to "https://gisserver.domain.com:6443/arcgis" instead of "http://gisserver.domain.com:6080/arcgis". This was to let users know that System Log Parser supports HTTPS. Using HTTP to connect to an ArcGIS Server host on port 6080 will still work.
2. WMTSTile support has been added for IIS log uploads into ArcGIS Monitor
3. Fixed a timing issue to help prevent the potential for log file read overlaps when uploading data into ArcGIS Monitor

Build 0.6.1.3 (Prerelease)
--------------
1. When setting up System Log Parser as a ArcGIS Monitor Task, the "Test" operation would incorrectly fail with "System.InvalidOperationException: Sequence contains no elements" if there were no IIS or ArcGIS server entries found for the default time frames.
   This output has now been corrected to return the appropriate JSON body.

Build 0.6.1.2 (Prerelease)
--------------
1. The default log verbosity setting in the Preferences.xml file has been changed from 'Warn' to 'Off'

Build 0.6.1.1 (Prerelease)
--------------
1. Fixed an issue where the report could not be created and would return the message "The given path's format is not supported" due to an illegal character
2. Fixed an issue in the ErrorsOnly Analysis Type report where some messages would still get truncated if they were longer than 150 characters

Build 0.6.1.0 (Prerelease)
--------------
1. Added enhancements for the integration of System Log Parser to ArcGIS Monitor for both IIS and ArcGIS payloads
2. Added a new command line version of System Log Parser called slp.exe that optimizes System Log Parser to ArcGIS Monitor communication. The existing command line features of "System Logs.exe" remain for backward compatibility.
3. Added ability to temporally show errors (errors with respect to time) with the ErrorsOnly Analysis Type report. Open the Preferences.xml file and set the <IsListErrorsTemporally>false</IsListErrorsTemporally> configuration to true. Restart System Log Parser.
4. Fix errors messages longer than 150 characters from being truncated in the ErrorsOnly Analysis Type report
5. Upgraded the internal EPPlus spreadsheet library to version 4.1 in order to increase the speed of creating large tables (errors/elapsed time tables)
6. Updated/simplified the command line help
7. The SystemMonitorConfiguration section in the Preferences file is a now deprecated feature and will no longer be supported with future releases of System Log Parser since newer installations of ArcGIS Monitor (v3.0+) handle the passing in of this information automatically
8. Added a "busy cursor" for ArcGIS Server and Web queries for improved application feedback

Build 0.6.0.0 (Prerelease)
--------------
1. Removed Log Level from GUI. This setting had no functionality impact
2. Removed Warnings and Error worksheet from Complete report in order to improve speed
3. Warnings and Error worksheet is now its own report. This report is created when the new Analyst Type called 'ErrorsOnly' is selected
4. Redesigned Warnings and Error report to be faster, more detailed and more accurate
5. Redesigned the individual service worksheets in the Complete report into one comprehensive worksheet called "All Service Elapsed Times" which has a table containing all ArcSOC elapsed times. Users can then filter for specific service and just create the chart(s) they need. This can help reduce the Excel generation time and keeps the file size down of the report.
6. The <IsChartThroughput> option in the Preferences.xml file is now obsolete due to the table in the "All Service Elapsed Times" worksheet
7. Removed 'WithOverviewCharts' from the Analysis Type list. For backwards compatibility in command-line scripts, selecting this as an Analysis Type will default to 'Complete'.
8. Fixed incorrect exit code when uploading to ArcGIS Monitor when an error was encountered
9. Improved verbosity (log and screen) if System Log Parser encounters any http errors
10. System Log Parser now treats most of the supporting http calls (which help provide additional but not critical information in the report) as non-fatal. Prior builds would stop if an error was encountered.
11. Fixed issue where some supporting http calls would not honor the timeout settings of the System Log Parser Preferences.xml file
12. Added ServerURL to the Preferences.xml file. For convenience, this can be "preset" to one specific, frequently used URL
13. Fixed issues that can crash System Log Parser when some command line options were specified but their input values omitted
14. Increased display time of the command line Help window before auto closing
15. SLP IIS to SM improvements such as immediate console feedback (used internally by ArcGIS Monitor) and individual IIS request uploads
16. Fixed issue where SLP now no longer examines each service for the EnhancedSiteReport feature if SystemMonitor is selected as the ReportType. This helps speed up the SystemMonitor upload execution.
17. Added the "Requests over Time" worksheet to the 'Complete' Analysis Type which charts the requests as they occurred over either 24hrs or 1week (depending on the given timeframe)
18. Fixed an issue where the IsEnhancedSiteReport routine would honor the cancellation of a report generation
19. In the report, the ArcGIS Server Build number was added along with the listing of the ArcGIS Server Version number
20. Various internal code cleanup/optimizations

Build 0.5.1.1 (Prerelease)
--------------
1. Fixed an issue with the -o flag which under certain conditions would not honor the value passed in and would open up the report even if the user passed in the command line argument of "-o false"

Build 0.5.1.0 (Prerelease)
--------------
1. Fixed issue with the new IsEnhancedSiteReport feature (e.g. the Site Service Details worksheet) where the report would not generate if this process encountered a service type of WMServer, GlobeServer or FeatureServer. IsEnhancedSiteReport property is now set to true in Preferences file for new installations...a simple workaround for this issue was to just set the IsEnhancedSiteReport property to false and restart System Log Parser.
2. Fixed issue attempting to open the License Agreement (the E204_2014-06.docx file) from the About System Log Parser window
3. Added the MaxRecordCount listing to the Site Service Details worksheet for services that support this property

Build 0.5.0.0 (Prerelease)
--------------
1. System Log Parser is now Prerelease! Refer to the license page during installation or the E204_2014-06.docx file post-installation.
2. Added an enchancement to the Web (IIS) report to list counts for HTTP 2XX - HTTP 5xx requests
3. Fixed Web report labeling to not recommend checking ArcGIS Server if no log entries were found in IIS

Build 0.4.3.0
--------------
1. The IsEnhancedSiteReport option is now set to true for newly created Preference files. The IsEnhancedSiteReport performs additional queries against ArcGIS Server (not against the logs) in order to determine several specific service configuration settings. This information is also displayed in the report.
2. Full support for the ltag parameter when parsing a Web log and sending it to ArcGIS Monitor. The ltag parameter is "log tag" option which helps ArcGIS Monitor internally with the grouping the specific log data.

Build 0.4.2.1
--------------
1. Adjusted the column header comments and arraingment for the Web (IIS) report
2. Fixed small bug in the ArcGIS Server log report where Identify requests would show up as two different items if a Complete or WithOverviewCharts Analysis Type report was selected
3. Fixed issue where the Web (IIS) report would always count the requests in the logs even if they were not a status code of 200 or 300. 
   W3C field of Protocol Status (sc-status) is not required but highly recommended to include as it improves this accuracy in the report.
   With this version, the following are required in the IIS log in order to be parsed by System Log Parser:
		i.    Date (date)
		ii.   Time (time)
		iii.  Client IP Address (c-ip)
		iv.   User Name (cs-username)
		v.    Server IP Address (s-ip)
		vi.   URI Stem (cs-uri-stem)
		vii.  Time Taken (time-taken)
   The following fields are recommended to also be included in the IIS log:
		i.    Protocol Status (sc-status)
4. Improved the warning message clarity in text report if the ArcGIS Server logs did not contain any service requests for the given time duration
5. Updated the System Log Parser Help

Build 0.4.2.0
--------------
1. Added new feature to auto-detect the IIS log column availability matchup...no need to select the exact 15 specific set of fields in the W3C format. 
	* However, System Log Parser will require that at least the following fields are available in the IIS log:
		i.    Date (date)
		ii.   Time (time)
		iii.  Client IP Address (c-ip)
		iv.   User Name (cs-username)
		v.    Server IP Address (s-ip)
		vi.   URI Stem (cs-uri-stem)
		vii.  Time Taken (time-taken)		
2. System Log Parser does not require that the "Use local time for file naming and rollover" option In the IIS Log File Rollover section be selected
3. Added Preference to group the map cache tiles requests in the Web log based on the Level of Detail...this can help shorten the Web (IIS) report
4. Improved the warning message clarity in Excel report if the ArcGIS Server logs did not contain any service requests for the given time duration
5. Filtered the warning/error worksheet in the Excel report to be more specific to just warnings and errors

Build 0.4.1.0
--------------
1. Fix axis labeling for several charts from the Analysis Type of WithOverviewCharts.
2. Added command line option to validate the ArcGIS Server logs or Web logs upload to Esri ArcGIS Monitor 3.0. With this option specified the ArcGIS Monitor Server URL is only validated...the log payload is not persisted (by design). 
3. Corrected a few minor bugs for the Web Logs payload sent to Esri ArcGIS Monitor 3.0
4. If System Log Parser is run from the command line and encounters and error, the runtime will issue an Exit of 1 instead of 0 (which generally signifies that the operation completed successfully)

Build 0.4.0.0
--------------
1. System Log Parser now has the ability to parse web logs. Currently this is limited to IIS and has the following requirements
	a. The Log File is in the W3C format 
	b. Use local time for file naming and rollover is checked
	c. The Log File format is W3C and has the following fields selected:
		i.    Date (date)
		ii.   Time (time)
		iii.  Client IP Address (c-ip)
		iv.   User Name (cs-username)
		v.    Server IP Address (s-ip)
		vi.   Server Port (s-port)
		vii.  Method (cs-method)
		viii. URI Stem (cs-uri-stem)
		ix.   URI Query (cs-uri-query)
		x.    Protocol Status (sc-status)
		xi.   Protocol Substatus (sc-substatus)
		xii.  Win32 Status (sc-win32-status)
		xiii. Time Taken (time-taken)
		xiv.  User Agent (cs(User-Agent))
		xv.   Referer (cs(Referer))
2. The ArcGIS Server charts in the report (when used with the Analyst Type of WithOverviewCharts or Complete) have been reworded in the interest of simplification and clarity
3. Support for sending the output of the ArcGIS Server logs or Web logs to Esri ArcGIS Monitor 3.0 (see ArcGIS Monitor 3.0 Help for details)

Build 0.3.6.0
--------------
1. Set 'Simple' to the default Analysis Type
2. In order to improve on log query performance, the QueryFilter used in the Preferences is overridden if 'Simple' is used an only log items with a code of 100004 (e.g. ArcSOC elapsed times) are retrieved. This can greatly shorten the query time.
3. Removed 'WithServiceCharts' from the Analysis Type list. For backwards compatibility in command-line scripts, selecting this as an Analysis Type will default to 'Complete'.
4. Increased application logging to aide with troubleshooting. Set the AppLogLevel tag in the Preferences to Info to increase application log verbosity.
5. Added ArcGIS Server's LogLevel and FileAge to the report
6. Moved the 'Max' column of the ArcSOC Elapsed time tabular view to the right so it is displayed immediately after P99

Build 0.3.5.4
--------------
1. Added some initial support for application logging
2. Fixed issue where the throughput chart (if enabled) would not render correctly and the times would be off by hour
3. Fixed issue where clicking cancel during a log query would not stop the query
4. Added better handling of an invalid Preferences file or invalid markup in the Preferences file
5. Enabled chart throughput rendering (up to 1 day) if a Complete Analysis Type is selected. Prior versions needed this option to also be set in the Preferences.

Build 0.3.5.2
--------------
1. Altered the internal storage format of the elapsed time floating point numbers from the logs to better account for international deployments. This now helps put the presentation format of Service Summary table on the viewing Spreadsheet program which is better equipped to honor the client environment's locale settings.

Build 0.3.5.1
--------------
1. Increased the error verbosity within the GUI when attempting to parse the ArcGIS Server ArcSOC elapsed time entries within the logs

Build 0.3.5.0
--------------
1. Added support to optionally create and store encrypted username and password Credential Sets within System Log Parser. Credential Sets allow you to reference a username and password by a string name that you can create through the GUI. For increased security, the username and password are encrypted before being saved. Automative scripts can then just reference the Credential Set by name.
2. Added '103800' to the default query filter
3. Enhanced the "Warning and Error Message Statistics" and "Map Server Request Statistics" tables so they are more informative
4. Updated the Help to cover the two new authentication options (Windows Authentication and Credential Set Authentication)
5. Fixed a bug that might cause System Log Parser to crash when run from the command line for certain versions of Windows

Build 0.3.4.0
--------------
1. Added support to optionally use Windows Authentication to a Web Adaptor endpoint (as opposed to passing in a username and password to the 6080/6443 endpoint). This can aide deployments that do not want to store the username/password in automative scripts but does require the Web Adaptor and ArcGIS Server to be configured for Windows Authentication at the Web tier.
2. Added support to the GUI to auto create the specified Output Directory if it does not exist
3. Added support to the GUI to check the specified output directory for write permission by the current user before starting the log query
4. Increased the size of the command line window to make the (command line) help easier to read. The command line help can be seen when System Log Parser is passed the "-h" option (from the command line).
5. Fixed the command line defaults to better match the GUI defaults

Build 0.3.3.3
--------------
1. Simplified the System Log Parser Help. The ability to configure the optional System Log Parser repository storage feature for use as a ArcGIS Monitor Extension is now performed through Esri Professional Services. If you are interested in this optional feature, please contact Esri Professional Services.

Build 0.3.3.2
--------------
1. Installation now includes template bat script referenced in Help documentation for easily sending log information to ArcGIS Monitor as needed. 

Build 0.3.3.1 
--------------
1. Fixed condition where selecting the Analysis Type of Simple still performed the logic for the other types but just did not add them to the report. Selecting Simple now does not do any of the other logic which can (slightly) speed up the report generation and potential avoid warnings from the tool (if warnings happened to be encountered with the other analysis types).
2. Clarified some references of the System Log Parser tool by name in the documentation 

Build 0.3.3.0 
--------------
1. Fixed User Overview worksheet...User Count per Unique "Service Method Machine User" chart was plotting number of user occurrences, it now plots the "service method machine user" metric correctly
2. Separated Service chart from SMMU (Service Method Machine User) chart
3. Made Overview charts easier to read and added verbal descriptions
4. Enhanced the "User Count per 'Service Method Machine User'" chart so its more informative
5. Added Count Percentages and Sum Percentages to the Service Summary table. These new columns let analyst quickly see which items are being requested the most as well as taking the most ArcSOC CPU.
6. Add a Preferences option to plot throughput (requests/sec) along with ArcSOC Elapsed Time if an Analysis Type of "Complete" was selected and the log query time period is 2 hours or less.
7. Fixed condition where date time data going into a ArcGIS Monitor could be off 20 minutes with respect to the local time.
8. Fixed case where the Request Statistics worksheet could encounter problems attempting to parse the map scales
9. Added more support (detailed documentation) for sending captured ArcGIS Server log data to a ArcGIS Monitor repository
10. Increased the "Log Messages per Query Page" default setting from 1000 to 9999 in order to help increase the performance of heavy log queries. Instead of using many smaller queries to generate a report System Log Parser now uses fewer, larger queries.

Build 0.3.2.0 
--------------
1. Added some support to send captured ArcGIS Server log data to a ArcGIS Monitor repository
2. Fixed datetime representation of log data such that when viewed in ArcGIS Monitor it is in the timezone of the machine running System Log Parser 
3. Added '0' and '8000' to the default query filter

Build 0.3.1.0 
--------------
1. Added a human readable DateTime column to the individual service charts that's dynamically formatted based on the given timespan and specifically used for making the charts easier to read
2. Added an additional Statistics page in the report called Request Statistics that lists information on the top 3 most requested map sizes and map scales. Note: currently, this only reports on REST export map and WMS requests.
3. Allowed System Log Parser Installer to automatically upgrade itself over an older version
4. Added '80014' to the default query filter
5. Fixed sizing on Back To Service Summary link

Build 0.3.0.0 
--------------
1. Added log error analysis which displays grouped error messages and a numeric count of their occurrence
2. Added the Machine Overview chart which breaks down the activity of serviced requests by machine (and cluster)
3. Added support for a Preferences file
	a) Added the option to specify a default value (in seconds) for the request timeout. This had a fixed value of 100 seconds which was encountered for some environments and caused the log query to stop prematurely.
	b) Added the option to specify a default value (in minutes) for the token expiration. The default ArcGIS Server value was encountered for some environments and could also cause the log query to stop prematurely.
	c) Added the option to specify the default column to sort by in the main Service table (e.g. on the Service Summary worksheet)
	d) Added the option to customize a specific list of ArcGIS Server codes to search when querying the logs
	e) Note: There are additional options in the Preferences file, but these other settings are currently unsupported
4. Changed default Analysis Type to WithOverviewChart to improve the generation speed of default report
5. Fixed an issue where "Add/Remove Programs" in Windows would show the incorrect installed version of System Log Parser
6. Corrected Starttime initialization value. Previous version based Starttime on "now", but it should be based on "now - the specified Endtime".
7. Added an "About System Log Parser" button (the blue exclamation point) on the graphical user interface to easily find the current version of the program

Build 0.2.4.0 
--------------
1. In the interest of improved scalability and stability, the individual service chart worksheet naming convention was changed to use a GUID instead of the "partial service name" and "occurance number". 
2. Added ArcGIS Server Version to one of the informational items stored at the top of report
3. Added the option of a text file to the list of report outputs
4. Increased the maximum number of allowable service items to report on
5. Added an additional hyperlink pointing back to the Service Summary above the chart of each individual service worksheet 

Build 0.2.3.0 
--------------
1. Fixed issue where System Log Parser could not parse certain log query results from deployments of where the locale of ArcGIS Server was not set to 'US'.
2. Added option to adjust the Log Messages per Query Page.
3. Added weighted average column at the end of the Service/Source summary which calculates the weighted average of the average ArcSOC processing time.
4. Renamed some of the connection and log query statistics section headers (e.g. Average Log Inquiry Time Total Inquiry Time), so these items are less likely to be confused information pertaining to the Service/Source summary items (e.g. Count, Avg, Stdev, etc...).
5. Split the Overview worksheet into two parts for easier viewing: Services Overview and Users Overview.
6. Renamed and clarified the chart titles for the Services Overview and Users Overview charts.
7. Added the 'Request Count per "Service"' chart to the Services Overview page which lists the most popular service based on all the Methods that users requested. Alternatively, the 'Request Count per "Service Method Machine User"' chart lists the most popular service based on the most hits to each Service-Method-Machine-User item.
8. Increased the verbosity of the error message if System Log Parser was not able to deserialize the ArcGIS Server log contents.

Build 0.2.2.0 
--------------
Initial Public Release

