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

# Example:

Visit [this blog post](https://aftersync.com/blog/delta-tags-a-new-mechanism-for-efficiently-keeping-track-of-incremental-reloads-in-qlikview-and-qlik-sense) for a more in-depth example of implementing DeltaTags.

# Compatibility Note
Even though the tagging functionality has been available since QlikView 10, there were issues with how reliably these tags could be updated (reset and set) using the script, which prevented these operations from functioning correctly. Even with one of the first releases of QlikView November 2017, there were issues.

For this reason, the Delta Tags script is compatible starting with the following versions of QlikView and Qlik Sense, and any newer version.

* QlikView November 2017, SR5
* Qlik Sense April 2018

# License

```
/*******************                 Delta Tags                 ********************

The MIT License (MIT)

Copyright (c) 2018-2019 Miguel Ángel García - All Rights Reserved

This script is part of the Lean Data Processing Framework code bundle.

************************         www.aftersync.com         *************************
********************         www.leandataprocessing.com         ********************

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

********************		********************		*******************/
```
