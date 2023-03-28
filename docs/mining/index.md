# Mining

PacketCrypt is a _bandwidth hard proof of work_, this means it requires lots of bandwidth to mine.
Miners collaborate with one another by sending small messages (called _Announcements_ (often referred to as "anns")) and the
sending of these messages requires a large amount of _bandwidth_.

Miners who are working in collaboration with one another are members of a mining pool, therefore
all mining of PacketCrypt utilises mining pools.

PacketCrypt mining is split into two distinct stages:

- Announcement Mining (often referred to as "ann mining") - Using your CPU to create Announcements.
- Block Mining - Collecting Announcements from Announcement Miners and using them to mine blocks.

Block mining is typically done at the mining pool's datacenter, however Announcement mining can be
done from anywhere.

When people refer to mining PKT, they typically mean "announcement mining" (also know as "ann mining") rather than "block mining" (also known as "running a pool").