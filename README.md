# 802.15.4 MAC layer performance dataset

Predictable network performance is key in many low-power wireless sensor network applications.
The *802_15_4_MAC_perf* datasets is a repository that stores measurements collected from the wilab2 testbed facility in Ghent about the MAC layer performance in IEEE 802.15.4 networks, and can be used for different statistical learning approaches.

## **Experiment setup**
To  understand  the  MAC-level packet delivery  performance several experiments in the wilab2 testbed have been set up. We used 28 RM090 nodes with an IEEE 802.15.4 radio organized in a star-like network topology, as shown on the figure below. All nodes use a CSMA/CA MAC protocol and periodically generate a 100 B message to a single receiver located in the center of the topology. The transmission power is  set  to  the  maximum, i.e. 5dBm,  to  ensure all nodes are in communication range.  To incorporate all factors that impact the MAC performance we setup several experiments varying the number of sending nodes (2-28 nodes), and the application traffic load (1pckt/2s, 1pckt/s, 2pckts/s, 4pckts/s, 8pckts/s, 16pckts/s and 64pckts/s).
We used an USRP B210 to generate controllable interference patterns by periodically transmitting a modulated carrier for 2ms, followed by a 8ms idle period.

![experiment_setup](https://cloud.githubusercontent.com/assets/7999611/21597995/51e8ae4a-d154-11e6-8984-554d0109b8b1.png)

## **Dataset description**
Two datasets are provided:
* a fine-granularity dataset with short-term MAC statistics over measurement periods of 5 seconds, located in the [dataset repository](#dataset-repository) location ./datasets/Training_data/802_15_4_MACperf_5s.csv, and 
* a coarse-granularity dataset with long-term MAC statistics collected over observation intervals with granularity of 30 seconds, located in the [dataset repository](#dataset-repository) location ./datasets/Testing_data/802_15_4_perf_30s.csv. Both datasets consist of the following environmental parameters and measured MAC performance metrics: node density, interference Indication, traffic load, throughput, packet loss, packet loss rate (PLR), packet reception rate (PRR).

**Dataset format**

The 802.15.4 MAC layer performance dataset consists of the following 8 columns, respectively: '*NumOfReceived*', '*PRR*', '*packetLoss*', '*PLR*', '*throughput*', '*IPI*', '*Density*', '*COR*', corresponding to the following MAC-level statistics:
* '*NumOfReceived*' is the number of received frames during a particular observation interval;
* '*PRR*' is the Packet Reception Rate, e.g. the percentage of received frames withing a particular observation interval;
* '*packetLoss*' is the number of erroneous frames within a particular observation interval;
* '*PLR*' is the Packet Loss Rate, i.e. the percentage of Lost frames withing a particular observation interval;
* '*throughput*' is the aggregated throughput of all sending nodes within a particular observation interval;
* '*IPI*' is the Inter-Packet-Interval of the transmitter expressed as *X*/128 (*seconds*), where *X* is the value in the '*IPI*' column;
* '*Density*' is the number of nodes that were active during the experiment observation interval;
* '*COR*' is the Channel Occupancy Ratio which indicates the level of interference generated, e.g. a level of 20 indicates an interference pattern periodically generated 20% of a time period, i.e. transmitting a modulated carrier for 2ms, followed by a 8 ms idle period.


## **How to use the dataset**

The MAC-level performance dataset can be loaded into a Pandas dataframe for easier further data manipulation using the following Python script:

```

'''
Created on Feb 3, 2017

This example script reads the recorded dataset.

@author: Merima Kulin
'''

import pandas as pd
import csv

def load_dataset(path):
    """
        Loads observations as Pandas Dataframe
        
        Args:
            path (str): path to the MAC performance statistics
        Returns:
            dataMatrix (df): data matrix
    """
    from pandas.parser import CParserError
    try:
        df = pd.read_csv(path)
        return df
        
    except CParserError:
        print(file, 'failed: check for header rows')

    except:
        print(file, 'failed: an error occurred')

if __name__ == '__main__':

	#Dataset file
	f="Path to the dataset"

	#Load data into pandas dataframe
	data=load_dataset(f)
	print(data)

```

## **Dataset repository**
For more details about the datasets and the experiments please refer to the 802_15_4MACperf dataset repository:
https://github.com/merimak/802_15_4MACperf_datasets

