This repo contains a test-script for use with Psychtoolbox-3 to
test VRR / FreeSync support of Linux 5.2 + AMD FreeSync gpu's.

Needs Psychtoolbox-3, e.g., on recent Debian or Ubuntu:

sudo apt-install octave-psychtoolbox-3

The included test script VRRTest was executed within GNU/Octave
on a amdgpu-wip-5.2 kernel to exercise VRR with different
test patterns within VRR range and below-the-range.

The PDF files contain various plots of the results when testing
on DCE-8, DCE-11 Polaris-11 and DCN-1 Raven Ridge.

You can run the tests yourself, either by launching octave
in interactive mode:

Terminal:  octave
In Octave: more off
           help VRRTest     % For help text with cmdline params.
           VRRTest('sine')  % For sine-wave test, 2000 flips.
           VRRTest('upstepping', 1000); % step up, 1000 flips.

Batch execution from terminal:
E.g.

octave --eval "VRRTest('sine')"

As can be seen from the PDF plots, DCN-1 Raven behaved very
well and robust even below VRR min, when lfc/btr was active.

With the additional BTR improvement patches:

DCE-8/DCE-11 behaved well within VRR range, and pretty ok
below min VRR for going from high to low frame durations,
and ok'ish for constant frame duration -- slowly converging
to target frame durations. Performance when going from low to
high frame duration was less than great.

Without the additional BTR patches, DCE-8/11 misbehaved whenever
below min VRR.

