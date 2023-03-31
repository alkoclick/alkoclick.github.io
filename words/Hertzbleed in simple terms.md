* CPUs regulate themselves, to run at their optimal frequency
* If a hard computation is going on, the CPU will bounce around (a bit higher and lower) its optimal operating point, and dynamically adjust itself. This may make it take longer to finish.
* Thus, any method of encryption that is vulnerable to a power analysis, is actually vulnerable to a timing analysis as well
* A curve model largely used in modern cryptography has a special case when there are anomalous inputs: It ouputs (x=y=0) which is not well defined
* This failure is propagated, so if in a sequence with 50 bits, bit #24 is anomalous, then all the following ones also get messed up


So...
* Based on the above, an attacker can target individual bits of the sequence to try and mess them up with anomalous input
* If they get messed up, then the algorithm outputs a sequence of 0
* The sequence of 0s is easier to compute, so the CPU goes brrrrrrr (fast)
* The algorithm terminates faster if the attacker has guessed successfully