#1 Sandboxing using jail, chroot, and depriv(2) -- which is our version of pledge.
   Also using veil(2) and unveil(2) to hide and unhide filesystem paths.

#2 Ktrace/Kdump (the original syscall tracing BSD tools) need to be reintegrated
   into OSX.  The "new ktrace" must  be removed or renamed nktrace (new ktrace).

   The old versions were:
	Binary ktrace.out files containing timestamps, function calls, parameters, 
        dereferenced parameters and return values.
        THINK TCPDUMP -W

   The new version of ktrace is completely different, and the old version is supplanted
   by the shitty dtruss which uses dtrace and requires root.

   Since when do you need to be root to trace a process?  Also, how come all of your 
   syscall output goes to stderr.  How is that helpful for debugging?

#3 IOKit fuzzing:
   Map input/output parameters for IOKit "method" functions.  Use "dumb" mutation-based fuzzing
   via interpolation and bitflips.  Use this in conjunction with snapshot fuzzing driven by a VM.
   VBox VM has support for this.

-- nujrzydvl
   MoD
   #phrack
