
While writing about how [Imperfect storage mediums are ideal](Imperfect%20storage%20mediums%20are%20ideal.md) I ended up making a comparison of human forgetting with data loss in storage mediums like SSDs.
The problem? I could not find a single number to draw a comparison. So... I ended up reading a bunch of things about how SSDs work, how to reduce their error rates, and all that jazz. 

So, here's things I learned about SSDs that were new to me:

* SSDs, contain blocks, which contain pages, which contain cells
* A NAND memory flash cell can contain less than 100 electrons
* A flash cell can contain a single value (SLC), or multiple values (MLC), double value (DLC, expressed as a single bit), or triple value (TLC, expressed as 2 bits), or quadruple (newest, QLC, 3 bits)
* Containing multiple values obviously doubles the capacity for each extra bit, but means it is easier to trigger Raw Bit Errors. The Raw Bit Error Rate metric is often used, abbreviatedd to RBER
* Reading and writing often wears cells out, but not accessing a cell for a very extended period of time (years) will slowly cause that value to degrade  
* Most SSDs use some form of error correction (ECC) which can catch and correct bits up to a failure threshold, above which the process completely fails and the values are considered unrecoverable
* For "offline", disconnected SSDs, a typical recommendation is to power them on at least once a year. If possible rewriting all data is a good step.
* SSDs leak current, especially when powered off. This leak increases for higher values per cell
* "A typical flash device is considered to be error-free if it guarantees an uncorrectable error rate of less than 10^-15, which corresponds to traditional data storage reliability requirements ... For an ECC that can correct up to 40 erroneous bits for every 1 KB of data, the acceptable RBER to meet this reliability requirement is 10^-3"
* SSDs do not like heat: The ambient data loss to current leak increases exponentially with temperature increase! Thus 50 degrees (C) means 27.5 faster aging than 20 degrees, and 90 degrees is 2100 times faster aging than 20! A phone left in the sun can easily hit 70 degrees.
* Magnetic media like tape or HDDs is a more reliable archival medium than eletric media. It is however also slower


Things I read:
* Data Longevity and Compatibility, https://web.ece.ucsb.edu/~parhami/pubs_folder/parh19f-ebdt-data-longevity-compatib.pdf
* Data Retention in MLC NAND Flash Memory: Characterization, Optimization, and Recovery, https://users.ece.cmu.edu/~omutlu/pub/flash-memory-data-retention_hpca15.pdf
* Bit Error Rate in NAND Flash Memories
* https://semiconductor.samsung.com/support/tools-resources/dictionary/semiconductors-101-part-3-inner-workings-of-the-ssd/
* https://www.threads.com/@innneresting/post/DUva13sDEEc
* https://forums.grc.com/threads/ssd-health-bit-rot-in-read-only-areas-is-quite-real-a-spinrite-opportunity.2003/