## problem statement
We found this [packet capture](https://challenge-files.picoctf.net/c_fickle_tempest/f208f7c58d3703ed5fe0a78f707f011fcbb8c0b210b35247762c7ccacb49fe46/capture.pcap). Recover the flag.

## Hint
none

## Solution
1. Open the ".pcap" file in wireshark.
2. Since the previous challenge involved following the UDP stream, that is the first step we should take to solve this. Go to `Analyze -> Follow -> UDP Stream` and click through the streams.
3. One stream has a message labeled start and the following streams are all strings of various lengths that contain the character "a".
4. Looking in the info column, we can see that the requests all come from different ports from the same IP.
5. Filter the IP: `ip.src == 10.0.0.66`
6. We can see that the second message originates from source port 5112. 112 is a number which should alert us, since its ASCII representation is `p`, which matches the flag template.
7. there two way you can do this which by running script or doing manually, 

if you want to do it manually which can do it If we then take the last 3 digits of each number in the order of the packet times and convert them to ASCII, we can get our flag.

here the script if you want it automatically

