# DeltaTags
An external QVS script for handling and tracking incremental loads (extract and transforms) in QlikView and Qlik Sense with QVD metadata

[Learn more here](https://aftersync.com/blog/delta-tags-a-new-mechanism-for-efficiently-keeping-track-of-incremental-reloads-in-qlikview-and-qlik-sense)

# About
DeltaTags is a technique for keeping track of incremental loads in QlikView and Qlik Sense that solves issues present in other existing approaches, while at the same time being highly efficient.

DeltaTags is suitable for identifying and handling changed data in QVDs, both on the Extract and Transform layers.

There are three major advantages to implementing Delta Tags:

* Reliability: It makes the delta process highly reliable, since the actual data being processed is no longer separated from the metadata used in the incremental logic (i.e. the “last refreshed timestamp”).
* Consistency: QVD files can be moved around, restored from backups, etc. This framework guarantees that, when a QVD is restored to a previous version or changed by an external process, the load script will automatically detect the delta timestamps on the restored file and reprocess the data accordingly.
* Efficiency: the Delta Tags approach also makes the incremental loads highly efficient since the metadata in QVDs can be quickly read from the load script and with minimal resource usage.

# How Delta Tags work
Here is a quick overview of how the process works:

1. First, at the beginning of the script, we configure the process so that it reads the tags in the input and output QVDs, and based on that determine the delta job timeframe.
2. The second step is to process the data based on the calculated timeframe. This is done similar to any other method and it doesn’t need to be modified.
3. Finally, at the end of the load script, before storing the QVD, field tags are set based on the new successful execution, so that they can be used the next time it runs.

# View it in Action:
Check out the video [here](https://youtube.com/watch/UEkFT4ZWFmc)

[![View it in action](http://img.youtube.com/vi/UEkFT4ZWFmc/maxresdefault.jpg)](https://youtube.com/watch/UEkFT4ZWFmc)

# Another Example:
Visit [this blog post](https://aftersync.com/blog/delta-tags-a-new-mechanism-for-efficiently-keeping-track-of-incremental-reloads-in-qlikview-and-qlik-sense) for a more in-depth example of implementing DeltaTags.

# Compatibility Note
Even though the tagging functionality has been available since QlikView 10, there were issues with how reliably these tags could be updated (reset and set) using the script, which prevented these operations from functioning correctly. Even with one of the first releases of QlikView November 2017, there were issues.

For this reason, the Delta Tags script is compatible starting with the following versions of QlikView and Qlik Sense, and any newer version.

* QlikView November 2017, SR5
* Qlik Sense April 2018
