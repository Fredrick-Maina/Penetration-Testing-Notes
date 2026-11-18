tools to use for packet analysis
## NetworkMiner
An open source Network Forensics Analysis Tool(NFAT).
   advantages over wireshark include:
   quick overview, traffic mapping and data extraction
   OS fingerprinting
   auto parameters/keyword discovery
   Host categorisation
   
   some cool features include:
   (hosts,files,images,messages,credentials,parameters, keyword) extractions,anomaly detection and many more.
   all these from just loading a pcap file.
 
## Brim 
 An open source desktop application that processes pcap fils and logs files. Its primary focus is providing search and analytics.
 - it uses zeek log processsing formaat, and also supports zeek signatures and suricata rules for detection.
 - it handles packet capture files and log flies
 - POWERFUL while processing big pcap files > 1GB
 - The common best practice is handling medium-sized pcaps with Wireshark, creating logs and correlating events with Zeek, and processing multiple logs in Brim.
 - 