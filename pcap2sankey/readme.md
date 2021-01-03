## Showing the byte-feature distribution of network packets which is  in a PCAP file with Sankey diagram

```python
from scapy.all import*
import os
```


```python

pkt = rdpcap("x.pcap")
```


```python
pkt[123].pdfdump("1.pdf")
```

    
    

![alt text](1.jpg)
