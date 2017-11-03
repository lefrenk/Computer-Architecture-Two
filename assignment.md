## The minimum seek time for an HDD is 9msec, and the maximum seek time is 90msec. The block size of this HDD is 4KB. How long on average does it take to read 100MB of data?

| 👇                  | #️⃣                 |
| --------------------|-------------------|
| Minimum seek time   | 9ms               |
| Maximum seek time   | 90ms              |
| Rotation rate       | 7200 RPM          |
| Transfer rate       | 157MB/second      |
| # sectors per track | 320               |
| Sector size         | 4096 bytes        |
| Controller overhead | 2.5ms (arbitrary) |

```
Given the formula:
seek time + rotational delay + transfer time + controller overhead

Average time to read a single sector (4096 bytes):
9 + (0.5 * 60 * 10^3 / 7200) + (4096 / (157 * 2^20)) * 1000 + 2.5 = 15.69ms

Average time to read 100MB (102,400,000 bytes):
9 + (0.5 * 60 * 10^3 / 7200) + (1024 * 10^5 / (157 * 2^20)) * 1000 + 2.5 = 637.68ms
```

Not factoring for multiple physical platters, multiple heads, or extra seek time due to disk fragmentation, the average read time for 100MB of data is 637.68ms on a 7200 RPM HDD with a 9ms seek time and a transfer rate of 157MB/s.

Transfer rate is calculated by multiplying the number of bytes per sector (4096) by the cylinder zone with the largest number of sectors (320). This is the number of bytes retrievable with one rotation of the disk (1,310,720 bytes). Multiply that by the number of rotations per second (7200 RPM / 60) = 120 * 1,310,720 = 157,286,400, or about 157 megabytes per second.

***

## Describe a TCP/IP packet in detail. Describe the header, how many bytes it is, and which components it contains. What data can come after the header?

Data that is sent over the Internet Protocol are split into __packets__ that contain a payload (segment of the data being transferred), an IP header and a TCP header.

The IP header includes the source IP address, destination IP address, and other metadata needed to route and deliver the packet: __protocol version__ (4-bits), __header length__ (4-bits), __types of service__ (8-bits), __total length__ (16-bits), __identification__ (16-bits), __flags__ (3-bits), __fragment offset__ (13-bits), __time to live__ (8-bits), __protocol__ (8-bits), __header checksum__ (16-bits), __source and destination IP__ (32-bits each), and __options__ which is of variable length.

The TCP header contains metadata that provides reliable, ordered, error-checked delivery of a stream of octets between applications.

Similar to the IP header, the TCP header is 20 bytes (160-bits) unless options are present. The TCP header contains the __source__ and __destination ports__ (16-bits each), 32-bit __sequence number__, 32-bit __acknoledgement number__, 4-bit __data offset__, 6-bits __reserved__ for future use, 6 __control__ bits (URG, ACK, PSH, RST, SYN, FIN), 16-bit __window__, 16-bit __checksum__, 16-bit __urgent pointer__.

__Options__ may come after the header and are a multiple of 8-bits in length.

***

## How does the network protocol guarantee that a TCP/IP packet is complete after transmission?

Each TCP/IP packet contains a __checksum__ in the TCP header. The value of the checksum is computed over the entire set of data. When the TCP segment arrives at its destination, the receiving end performs the same checksum calculation. If there is a mismatch between its calculation and the value of the __checksum__ field in the TCP header, this indicates an error of some sort occurred during transmission and the segment is normally discarded.

In addition, TCP/IP uses __IP fragmentation__, which is a process that breaks data into smaller fragments, so that packets may be formed that can pass through a link with a smaller maximum transmission unit (MTU) than the original data size.

When the packets are received by the receiving host, the fragments are identified by the __identification__ field (in the IP header) as belonging together. The __fragment offset__ field is then used to reassemble the fragments into their original IP payload.

***

## What is the difference between TCP and IP?

The __Transmission Control Protocol (TCP)__ corresponds to OSI Layer 4 (transport), which provides the delivery of a stream of bytes from a program from one computer to another computer. __TCP__ is also in charge of controlling size, flow control, the rate of data exchange, network traffic congestion, and as mentioned above, error-checking.

The __Internet Protocol (IP)__ corresponds to a subset of OSI Layer 3 (network). It's the principal communications protocol in the TCP/IP suite for relaying datagrams across network boundaries. Its routing function enables internetworking, which is the foundation of the Internet. __IP__ defines addressing methods and structures for the encapsulation of the packets.

***

## Why is 3d performance so much higher with a graphics card than without? Modern CPUs are extremely fast, what is limiting their performance?

Architecturally, a __CPU is composed of just a few cores__ with lots of cache memory that can handle a __few software threads that are optimized for sequential serial processing__. In contrast, a __GPU is composed of hundreds of cores that can handle thousands of threads simultaneously__.

The GPU’s advanced capabilities were originally used primarily for 3D game rendering. But now those capabilities are being harnessed more broadly to accelerate computational workloads in areas such as financial modeling, cutting-edge scientific research and oil and gas exploration.

👋