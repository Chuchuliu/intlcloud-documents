CCN is a pay-as-you-go service. 

- Interconnection of cross-region network instances incurs fees, so you may want to set a bandwidth limit in time.
- Interconnection below 1 Gbps of intra-region network instances is free of charge for the time being.

## Billing
<span id='moshi'></span>

### Billing Method
Cross-region interconnection cost of CCN is billed by the monthly 95th percentile (average bandwidth value is taken every 5 minutes in a natural month) based on the actually consumed bandwidth in each region.

**Cross-account Billing:**

The network instance (such as a VPC) of account A can be joined to the CCN instance of account B, and all the interconnection fees incurred are paid by the account of the CCN instance (i.e., account B), while account A does not need to pay any fees.

### Billing Formula

**Monthly CCN cost** = the sum of cross-region interconnection service fees incurred in each region of the network instances on CCN.

**Monthly single-region fee** = the monthly 95th percentile bandwidth peak for the region \* valid day proportion \* tiered unit price

Where:

- **The monthly 95th percentile bandwidth peak**
In a natural month, the average bandwidth value is taken every 5 minutes on each valid day (when bandwidth is consumed), then the taken average bandwidth values are sorted in ascending order with the highest 5% of the values removed, and the next highest value is used as the monthly 95th percentile bandwidth peak.
For example, if you use CCN in June and there are 14 valid days when cross-region interconnection is realized in region A, then the number of statistical points per day is 288 (60 min \* 24 / 5 min), and the number of all statistical points in the 14 days are 4032 (14 days \* 288 / day). The bandwidth values of the 4032 statistical points are sorted in ascending order, and the highest 5% of points are removed (4032 \* 0.95 = 3830.4), so the bandwidth value of the 3830th point is the monthly 95th percentile bandwidth peak which is recorded as Max 95.
- **Valid day proportion**
A valid day refers to a day when the bandwidth value of any 5-minute statistical point is greater than 3 Kbps, and the valid day proportion = the valid days in the month / the natural days in the month.
- **Tiered unit price**
A unit price in the tiered pricing scheme. For example, if the monthly 95th percentile bandwidth peak is 95 Mbps in a month, then the monthly fees = 95 \* tiered unit price [for 50-100 Mbps].

### Billing Example

Suppose that your CCN instance is associated with network instances in three regions: Guangzhou, Beijing and Shanghai.

![](https://main.qcloudimg.com/raw/4bdd0f76a2c721dddea4e904513c2c96.png)

Different from Peering Connection and Direct Connect which are billed based on inter-instance bandwidth, CCN is billed based on inter-region bandwidth. This document uses Guangzhou and Beijing as examples: 
In June, the bandwidth of VPC 1 in Guangzhou to VPC 2 and VPC 3 in Beijing is 50 Mbps, and the bandwidth of the Direct Connect gateway in Guangzhou to VPC 3 is 50 Mbps (as shown below). However, due to the presence of peaks and valleys, the final billable bandwidth between Guangzhou and Beijing will be 50-150 Mbps. If it is assumed to be 120 Mbps, the billable bandwidth generated by CCN between Beijing and Guangzhou is 120 Mbps (for calculation details, see [Billing Method](#moshi)).

![](https://main.qcloudimg.com/raw/65eee0f1741d405af652c4a57021fcd0.png)

Suppose that there are 14 valid days when interconnection is realized between Guangzhou and Beijing in June, then the CCN fee incurred by the interconnection between Guangzhou and Beijing in June is: billable bandwidth (120 Mbps) \* valid day ratio (14 / 30) \* tiered unit price (13USD/Mbps/month) = USD728.
Fees for other regions are calculated in a similar way (Guangzhou-Shanghai: USD1036; Beijing-Shanghai: USD518). The final CCN cost is the sum of the inter-region interconnection fees, namely 728 + 1036 + 518 = USD2282.
## Pricing Overview
CCN is pay-per-use based on the monthly 95th percentile bandwidth peak. The corresponding tiered unit prices of the specific bandwidth used in each region are as shown in the following table:

| From Mainland China to other regions                |              |          |                                                              |                                    |                  |                                        |
| --------------------------------- | ------------ | -------- | ------------------------------------------------------------ | ---------------------------------- | ---------------- | -------------------------------------- |
| Billing method                              | Tier         | Mainland China | Hong Kong, Korea (Seoul), Japan (Tokyo), Singapore, India (Mumbai), Thailand (Bangkok)  | Western America (Silicon Valley), Eastern America (Virginia) | Canada (Toronto) | Germany (Frankfurt), Russia (Moscow) |
| Billable bandwidth based on the 95th percentile (USD/Mbps/month) | 0-100 Mbps    | 37       | 151                                                          | 190                                | 190              | 175                                    |
|                                   | 100-1000 Mbps | 13       | 87                                                           | 111                                | 111              | 105                                    |
|                                   | 1000+ Mbps | 9        | 76                                                           | 95                                 | 95               | 83                                     |

| From Asia Pacific (Hong Kong, Korea, Japan, Singapore, India, Thailand) to other regions |              |          |                                                              |                                    |                  |                                        |
| ---------------------------------------------------------- | ------------ | -------- | ------------------------------------------------------------ | ---------------------------------- | ---------------- | -------------------------------------- |
| Billing method                                                       | Tier         | Mainland China | Hong Kong, Korea (Seoul), Japan (Tokyo), Singapore, India (Mumbai), Thailand (Bangkok)  | Western America (Silicon Valley), Eastern America (Virginia) | Canada (Toronto) | Germany (Frankfurt), Russia (Moscow) |
| Billable bandwidth based on the 95th percentile (USD/Mbps/month) | 0-100 Mbps    | 151      | 151                                                          | 151                                | 151              | 175                                    |
|                                                            | 100-1000 Mbps | 87       | 87                                                           | 87                                 | 87               | 105                                    |
|                                                            | 1000+ Mbps | 76       | 76                                                           | 76                                 | 76               | 83                                     |

| From Russia (Moscow) and Germany (Frankfurt) to other regions |              |          |                                                              |                                    |                  |                                        |
| -------------------------------------------- | ------------ | -------- | ------------------------------------------------------------ | ---------------------------------- | ---------------- | -------------------------------------- |
| Billing method                                         | Tier         | Mainland China | Hong Kong, Korea (Seoul), Japan (Tokyo), Singapore, India (Mumbai), Thailand (Bangkok)  | Western America (Silicon Valley), Eastern America (Virginia) | Canada (Toronto) | Germany (Frankfurt), Russia (Moscow) |
| Billable bandwidth based on the 95th percentile (USD/Mbps/month) | 0-100Mbps    | 175      | 175                                                          | 175                                | 175              | 151                                    |
|                                              | 100-1000 Mbps | 105      | 105                                                          | 105                                | 105              | 87                                     |
|                                              | 1000+ Mbps | 83       | 83                                                           | 83                                 | 83               | 76                                     |

| From Canada (Toronto) to other regions        |              |          |                                                              |                                    |                                        |
| --------------------------------- | ------------ | -------- | ------------------------------------------------------------ | ---------------------------------- | -------------------------------------- |
| Billing method                                             | Tier         | Mainland China | Hong Kong, Korea (Seoul), Japan (Tokyo), Singapore, India (Mumbai), Thailand (Bangkok)  | Western America (Silicon Valley), Eastern America (Virginia) | Germany (Frankfurt), Russia (Moscow) |
| Billable bandwidth based on the 95th percentile (USD/Mbps/month) | 0-100 Mbps    | 190      | 151                                                          | 121                                | 175                                    |
|                                   | 100-1000 Mbps | 111      | 87                                                           | 67                                 | 105                                    |
|                                   | 1000+ Mbps | 95       | 76                                                           | 60                                 | 83                                     |

| From Western America (Silicon Valley), Eastern America (Virginia) to other regions |              |          |                                                              |                                    |                  |                                        |
| ------------------------------------------------ | ------------ | -------- | ------------------------------------------------------------ | ---------------------------------- | ---------------- | -------------------------------------- |
| Billing method                                             | Tier         | Mainland China | Hong Kong, Korea (Seoul), Japan (Tokyo), Singapore, India (Mumbai), Thailand (Bangkok)  | Western America (Silicon Valley), Eastern America (Virginia) | Canada (Toronto) | Germany (Frankfurt), Russia (Moscow) |
| Billable bandwidth based on the 95th percentile (USD/Mbps/month) | 0-100 Mbps    | 190      | 151                                                          | 15                                 | 121              | 175                                    |
|                                                  | 100-1000 Mbps | 111      | 87                                                           | 9                                  | 67               | 105                                    |
|                                                  | 1000+ Mbps | 95       | 76                                                           | 7                                  | 60               | 83                                     |


>**Note:**
>If you need data interconnection between Mainland China and outside Mainland China regions, please consult your Tencent Cloud representative.
