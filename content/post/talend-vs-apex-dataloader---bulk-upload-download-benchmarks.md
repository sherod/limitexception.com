+++
author = "Steven Herod"
date = 2011-12-15T00:00:00Z
description = ""
draft = false
slug = "talend-vs-apex-dataloader---bulk-upload-download-benchmarks"
title = "Talend vs Apex Dataloader — Bulk upload/Download benchmarks"

+++


### Key Points

* Both [Data Loader](http://wiki.developerforce.com/page/Apex_Data_Loader) and [Talend](http://www.talend.com/index.php) use the same underlying APIs to Salesforce and have the same options (Batch size, compression enabling/disabling, use of bulk interface)
* There is little difference between Data Loader and Talend in overall performance
* There is a big difference between bulk vs non bulk upload and between using and not using compression.
* Salesforce is up to 2x faster at data retrievals than data inserts
* One constraint that has not been quantified is the effect of limited bandwidth on performance, it does matter, but I’m not sure how much.

ActivityToolCompressionBatch sizeTotal recordsRecords per secondRecords per hourNon bulk uploadTalendNo2005000196840Non bulk uploadTalendYes20050003914040Bulk uploadData LoaderN/A1000500015254720Bulk uploadTalendN/A1000 500013147160DownloadTalendYes100025000348125280DownloadData LoaderYes100025000303109400

