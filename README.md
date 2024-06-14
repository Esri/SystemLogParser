# System Log Parser
## Version 0.13.0.1
### Date: 2024/06/14

-------------------------------
### Download Latest Release
[**System Log Parser Download**](../../raw/main/binaries/latest/SystemLogParser.zip)

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

#### System Requirements
 - 64bit Windows Operating System:
	- Windows (Workstation): 7, 8*, 8.1**, 10**, 11**
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
- **If using Windows 8.1 or greater, the .NET Framework 3.5 (in addition to 4.8) must be enabled per Microsoft documentation
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
#### How To Download System Log Parser
- Download the latest release here:
[**System Log Parser Download**](../../raw/main/binaries/latest/SystemLogParser.zip)
and unzip it to your local workstation
- System Log Parser does not include an installer.

-------------------------------
#### How To Use System Log Parser
Once the System Log Parser is downloaded and unzipped, launch the GUI by double-clicking on SystemLogsGUI.exe
The most common scenario for using System Log Parser is to point it at an ArcGIS Server to analyze the logs:
- Once the this has launched, select the ArcGIS Server (Web) tab from the top
- Fill out the necessary information like Server URL and Authentication details
- Click Analyze
- System Log Parser will connect to ArcGIS Server to retrieve and analyze the logs, then produce a spreadsheet report
- The log retrieval make take a few moments, depending on the size of the ArcGIS Server logs
- The generated report can be used to help quantify the GIS usage of the Site by providing a breakdown of what services users are requesting and how long they are waiting for the response

Note: the ArcGIS Server LogLevel must be set to Fine when performing ArcGIS Server (Web) analysis

-------------------------------
#### Esri Community Articles on System Log Parser for Specific Scenarios
- [ArcGIS Enterprise Analysis with System Log Parser's Optimized Analysis Type](https://community.esri.com/t5/implementing-arcgis-blog/arcgis-enterprise-analysis-with-system-log-parser/ba-p/1189005)
- [Automating System Log Parser from the Windows Command Line](https://community.esri.com/t5/implementing-arcgis-blog/automating-system-log-parser-from-the-windows/ba-p/1195294)
- [ArcGIS Enterprise Analysis with System Log Parser's ServiceDetails Analysis Type](https://community.esri.com/t5/implementing-arcgis-blog/arcgis-enterprise-analysis-with-system-log-parser/ba-p/1198115)
- [System Log Parser - Statistics and Service Optimization](https://community.esri.com/t5/implementing-arcgis-blog/system-log-parser-statistics-and-service/ba-p/886389)
- [ArcGIS Server Tuning and Optimization with System Log Parser
](https://community.esri.com/t5/implementing-arcgis-blog/arcgis-server-tuning-and-optimization-with-system/ba-p/886361)

-------------------------------
##### License
System Log Parser is released under: CC BY-NC-SA 4.0
- [https://creativecommons.org/licenses/by-nc-sa/4.0/](https://creativecommons.org/licenses/by-nc-sa/4.0/)
- [https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode.en](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode.en)
<img src="/assets/images/by-nc-sa.png" width="202" height="71">

-------------------------------
##### Support Status
System Log Parser is not a supported tool

-------------------------------
##### ChangeLog
[ChangeLog details](https://github.com/ArcGIS/SystemLogParser/blob/main/CHANGELOG.md)
