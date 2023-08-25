# SSD vs HDD

Optimal thing is to use what I already have and optimize my current data usage.


# Cost per TB-Year

- Assume drive is pretty much always spun up (ZFS or mirroring).
- Assume SSD idle cost is $0, aka $3/decade ~= .1/1000*24*365*.34*10`
- Assume cost of watts is constant with inflation for the next decade, and we are working in 2023-dollars.


- 6 idle Watts-hours per hard drive == 6/1000 KWH / HDD
- 1 HDD * 8 Years == 6/1000 KWH/HDD * 24 hours/day * 365 days/year * 8 years == 420 KWH
- 420 KWH * 0.34/KWH = $142.80 lifetime cost

- $322.80 / 18TB HDD @ 8 year lifetime == $322.80 / 144 TB-YEAR == $2.24/TB-YEAR
- $150 / 4TB SSD @ 10 year lifetime == $150 / 40 TB-YEAR == $3.75/TB-YEAR


# GPT-4  Analyzes the requirements

Here's the final setup:

| Data Type        | Storage Type            | Capacity | Location                   | Special Functionality      |
|------------------|-------------------------|----------|----------------------------|----------------------------|
| Gaming Data      | M.2 NVMe SSD            | 2TB      | Gaming Computer            | N/A                        |
| Business Data    | M.2 NVMe SSD and 2.5" SSD in ZFS (mirroring) | 4TB  | Lenovo ThinkCentre M910q   | ZFS for data redundancy, Always-on |
| Media Data       | HDD in USB-C Enclosure  | 8TB      | Connected to Lenovo ThinkCentre M910q | N/A |


- GPT-3 Recommendation: Use a external USB HDD enclosure with a smart plug, orchestrate unpowering the smart plug with unmounting the device via bash script
  - Problem: Enclosures mainly do not power on when repowered, because they don't have mechanical switches.
  - Googled solution: However, external drive bays often do. I already have 1, but it doesn't seem great for constant use... I will prototype with it.
