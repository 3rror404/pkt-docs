# Mining

PKT is mined using a CLI applications called PacketCrypt. When people refer to "the miner", "miner" or "PKT miner" they typically mean PacketCrypt.

There are also two other pieces of sofware that can be used to mine PKT Cash: 
1. The PKT World wallet which has an inbuilt miner.
2. Minr, which is a simple to use application built by pkt.watch.

PacketCrypt is a bandwidth hard proof of work, this means it requires lots of bandwidth to mine.
Miners collaborate with one another by sending small pieces of data (called Announcements (often referred to as "anns")) to mining pools and the sending of these announcements requires a large amount of bandwidth.

Miners who are working in collaboration with one another are members of a mining pool, therefore
all mining of PacketCrypt utilises mining pools.

PacketCrypt mining is split into two distinct stages:

- Announcement Mining (often referred to as "ann mining") - Using your CPU to create Announcements.
- Block Mining - Collecting Announcements from Announcement Miners and using them to mine blocks.

Block mining is typically done at the mining pool's datacenter, however Announcement mining can be
done from anywhere.

When people refer to mining PKT, they typically mean "announcement mining" (also know as "ann mining") rather than "block mining" (also known as "running a pool").