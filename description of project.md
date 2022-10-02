# SNA Group Assignment

Importing Libraries


```python
import networkx as nx
import pandas as pd
import matplotlib.pyplot as plt
```

Importing dataset


```python
users = pd.read_csv('musae_git_target.csv')
```

Reading Graphs


```python
Data = open('musae_git_edges.csv', "r")

next(Data, None)  # skip the first line in the input file

followers = nx.parse_edgelist(Data, delimiter=',', create_using=nx.Graph(), nodetype=int)
```

Finding Local Cluster (each nodes clustering coefficient)


```python
local_cluster = nx.clustering(followers)
sorted_local_cluster = {k: v for k, v in sorted(local_cluster.items(), key=lambda item: item[1])}
sorted_local_cluster
```




    {0: 0,
     34526: 0,
     34035: 0,
     6067: 0,
     20183: 0,
     3: 0,
     4950: 0,
     4: 0,
     2865: 0,
     5: 0,
     22674: 0,
     29465: 0,
     30833: 0,
     17: 0,
     36632: 0,
     291: 0,
     21498: 0,
     327: 0,
     27954: 0,
     25948: 0,
     1268: 0,
     28: 0,
     13003: 0,
     32: 0,
     34: 0,
     27804: 0,
     25218: 0,
     1524: 0,
     9804: 0,
     32139: 0,
     24921: 0,
     37463: 0,
     24033: 0,
     14266: 0,
     5338: 0,
     9349: 0,
     6185: 0,
     27718: 0,
     8608: 0,
     44: 0,
     45: 0,
     12703: 0,
     30789: 0,
     9946: 0,
     33324: 0,
     33602: 0,
     48: 0,
     26597: 0,
     7121: 0,
     30074: 0,
     22212: 0,
     54: 0,
     36103: 0,
     5568: 0,
     57: 0,
     59: 0,
     60: 0,
     37077: 0,
     62: 0,
     63: 0,
     29946: 0,
     64: 0,
     29440: 0,
     26706: 0,
     70: 0,
     6078: 0,
     2819: 0,
     5880: 0,
     23139: 0,
     77: 0,
     79: 0,
     82: 0,
     25858: 0,
     8828: 0,
     5858: 0,
     84: 0,
     18373: 0,
     33824: 0,
     90: 0,
     21351: 0,
     15808: 0,
     91: 0,
     23110: 0,
     1337: 0,
     21912: 0,
     13576: 0,
     21993: 0,
     93: 0,
     13506: 0,
     95: 0,
     6081: 0,
     18835: 0,
     14459: 0,
     23519: 0,
     6082: 0,
     6114: 0,
     34423: 0,
     21537: 0,
     7183: 0,
     32897: 0,
     102: 0,
     20132: 0,
     15541: 0,
     27903: 0,
     111: 0,
     112: 0,
     8459: 0,
     11793: 0,
     16315: 0,
     31631: 0,
     2993: 0,
     13790: 0,
     21081: 0,
     31829: 0,
     19012: 0,
     10194: 0,
     5224: 0,
     30483: 0,
     2164: 0,
     5943: 0,
     121: 0,
     122: 0,
     23733: 0,
     127: 0,
     22898: 0,
     128: 0,
     7607: 0,
     34696: 0,
     26568: 0,
     30936: 0,
     6421: 0,
     15861: 0,
     136: 0,
     9040: 0,
     19752: 0,
     1808: 0,
     18682: 0,
     138: 0,
     26996: 0,
     19217: 0,
     23013: 0,
     18786: 0,
     9775: 0,
     6997: 0,
     142: 0,
     19300: 0,
     22137: 0,
     148: 0,
     26499: 0,
     149: 0,
     151: 0,
     152: 0,
     28970: 0,
     4016: 0,
     153: 0,
     154: 0,
     25844: 0,
     9520: 0,
     2796: 0,
     32914: 0,
     35158: 0,
     28434: 0,
     28474: 0,
     16567: 0,
     12963: 0,
     11394: 0,
     32559: 0,
     29598: 0,
     37522: 0,
     11182: 0,
     31802: 0,
     160: 0,
     16101: 0,
     165: 0,
     167: 0,
     21840: 0,
     169: 0,
     170: 0,
     35714: 0,
     172: 0,
     173: 0,
     27685: 0,
     21802: 0,
     5402: 0,
     7360: 0,
     15748: 0,
     1427: 0,
     6968: 0,
     10730: 0,
     183: 0,
     186: 0,
     6095: 0,
     188: 0,
     25152: 0,
     9892: 0,
     24060: 0,
     18266: 0,
     30836: 0,
     195: 0,
     1163: 0,
     35794: 0,
     202: 0,
     204: 0,
     206: 0,
     24228: 0,
     207: 0,
     209: 0,
     1236: 0,
     211: 0,
     217: 0,
     37206: 0,
     3664: 0,
     2074: 0,
     22370: 0,
     6044: 0,
     24031: 0,
     25279: 0,
     33010: 0,
     27629: 0,
     220: 0,
     221: 0,
     20901: 0,
     222: 0,
     10688: 0,
     13022: 0,
     8228: 0,
     8191: 0,
     15980: 0,
     22132: 0,
     225: 0,
     30674: 0,
     13245: 0,
     35572: 0,
     25007: 0,
     1573: 0,
     229: 0,
     35599: 0,
     234: 0,
     238: 0,
     4630: 0,
     34169: 0,
     245: 0,
     24535: 0,
     37540: 0,
     33127: 0,
     247: 0,
     248: 0,
     252: 0,
     256: 0,
     13675: 0,
     14296: 0,
     259: 0,
     24539: 0,
     36180: 0,
     263: 0,
     3138: 0,
     267: 0,
     268: 0,
     270: 0,
     2147: 0,
     1013: 0,
     13772: 0,
     32661: 0,
     280: 0,
     23354: 0,
     9753: 0,
     33423: 0,
     283: 0,
     17717: 0,
     27608: 0,
     286: 0,
     287: 0,
     36540: 0,
     289: 0,
     28144: 0,
     36774: 0,
     32120: 0,
     18967: 0,
     292: 0,
     1037: 0,
     25288: 0,
     6657: 0,
     32215: 0,
     299: 0,
     300: 0,
     36957: 0,
     301: 0,
     32311: 0,
     304: 0,
     306: 0,
     20910: 0,
     3123: 0,
     31358: 0,
     26982: 0,
     11707: 0,
     27739: 0,
     315: 0,
     3360: 0,
     317: 0,
     23680: 0,
     27177: 0,
     17030: 0,
     11977: 0,
     18114: 0,
     322: 0,
     31920: 0,
     11961: 0,
     33274: 0,
     680: 0,
     31218: 0,
     329: 0,
     21339: 0,
     330: 0,
     13208: 0,
     331: 0,
     22294: 0,
     334: 0,
     27893: 0,
     30193: 0,
     4125: 0,
     27919: 0,
     339: 0,
     341: 0,
     6964: 0,
     354: 0,
     355: 0,
     18362: 0,
     4094: 0,
     3645: 0,
     16347: 0,
     36385: 0,
     19247: 0,
     901: 0,
     23476: 0,
     31772: 0,
     16276: 0,
     9198: 0,
     32480: 0,
     16731: 0,
     367: 0,
     369: 0,
     2029: 0,
     370: 0,
     372: 0,
     374: 0,
     375: 0,
     22216: 0,
     6187: 0,
     379: 0,
     380: 0,
     381: 0,
     382: 0,
     384: 0,
     385: 0,
     387: 0,
     33371: 0,
     390: 0,
     10933: 0,
     391: 0,
     392: 0,
     395: 0,
     19229: 0,
     1500: 0,
     37140: 0,
     3125: 0,
     24278: 0,
     907: 0,
     2715: 0,
     14980: 0,
     22865: 0,
     3044: 0,
     1858: 0,
     4443: 0,
     27560: 0,
     30221: 0,
     405: 0,
     406: 0,
     17903: 0,
     410: 0,
     33197: 0,
     3394: 0,
     414: 0,
     6098: 0,
     21811: 0,
     6247: 0,
     22522: 0,
     6704: 0,
     33999: 0,
     28226: 0,
     3103: 0,
     11867: 0,
     424: 0,
     22250: 0,
     15731: 0,
     22919: 0,
     10579: 0,
     35706: 0,
     9146: 0,
     37632: 0,
     428: 0,
     429: 0,
     6731: 0,
     20931: 0,
     434: 0,
     436: 0,
     20589: 0,
     4941: 0,
     18766: 0,
     30457: 0,
     449: 0,
     33956: 0,
     33931: 0,
     17900: 0,
     32016: 0,
     34778: 0,
     16825: 0,
     33949: 0,
     36272: 0,
     689: 0,
     461: 0,
     556: 0,
     462: 0,
     12444: 0,
     35833: 0,
     24202: 0,
     28517: 0,
     472: 0,
     26895: 0,
     474: 0,
     12124: 0,
     475: 0,
     36978: 0,
     476: 0,
     909: 0,
     29725: 0,
     20647: 0,
     30942: 0,
     484: 0,
     485: 0,
     487: 0,
     488: 0,
     489: 0,
     6835: 0,
     4061: 0,
     3010: 0,
     16757: 0,
     11624: 0,
     13098: 0,
     34534: 0,
     24414: 0,
     31136: 0,
     28668: 0,
     4952: 0,
     24078: 0,
     3310: 0,
     10116: 0,
     29276: 0,
     30260: 0,
     499: 0,
     1784: 0,
     7278: 0,
     505: 0,
     6591: 0,
     510: 0,
     511: 0,
     27603: 0,
     517: 0,
     15566: 0,
     24667: 0,
     11595: 0,
     2905: 0,
     519: 0,
     16346: 0,
     520: 0,
     698: 0,
     11783: 0,
     523: 0,
     16089: 0,
     525: 0,
     31589: 0,
     528: 0,
     37058: 0,
     533: 0,
     23468: 0,
     18446: 0,
     6740: 0,
     544: 0,
     33840: 0,
     22670: 0,
     11069: 0,
     28384: 0,
     32319: 0,
     32237: 0,
     14929: 0,
     36845: 0,
     25490: 0,
     27852: 0,
     32641: 0,
     18765: 0,
     12738: 0,
     17483: 0,
     31088: 0,
     1423: 0,
     36415: 0,
     564: 0,
     565: 0,
     566: 0,
     16725: 0,
     570: 0,
     572: 0,
     7784: 0,
     3558: 0,
     575: 0,
     8108: 0,
     27253: 0,
     2548: 0,
     579: 0,
     580: 0,
     1433: 0,
     31015: 0,
     36345: 0,
     23633: 0,
     36174: 0,
     594: 0,
     6088: 0,
     598: 0,
     34393: 0,
     600: 0,
     1035: 0,
     32186: 0,
     604: 0,
     29406: 0,
     608: 0,
     10169: 0,
     25203: 0,
     20424: 0,
     613: 0,
     22483: 0,
     614: 0,
     616: 0,
     16144: 0,
     13302: 0,
     622: 0,
     29534: 0,
     624: 0,
     33232: 0,
     32169: 0,
     628: 0,
     629: 0,
     15874: 0,
     632: 0,
     32610: 0,
     21186: 0,
     31524: 0,
     25881: 0,
     636: 0,
     20120: 0,
     637: 0,
     638: 0,
     6168: 0,
     640: 0,
     35628: 0,
     28678: 0,
     34159: 0,
     29484: 0,
     15422: 0,
     14467: 0,
     36881: 0,
     14508: 0,
     36314: 0,
     649: 0,
     653: 0,
     654: 0,
     35920: 0,
     656: 0,
     657: 0,
     660: 0,
     27547: 0,
     19323: 0,
     662: 0,
     663: 0,
     21084: 0,
     669: 0,
     31919: 0,
     673: 0,
     674: 0,
     18185: 0,
     29284: 0,
     18917: 0,
     676: 0,
     677: 0,
     34697: 0,
     7150: 0,
     24300: 0,
     684: 0,
     687: 0,
     688: 0,
     16213: 0,
     3299: 0,
     6490: 0,
     28768: 0,
     693: 0,
     25745: 0,
     27891: 0,
     4477: 0,
     696: 0,
     697: 0,
     35344: 0,
     701: 0,
     704: 0,
     30184: 0,
     17711: 0,
     26928: 0,
     6678: 0,
     17841: 0,
     34247: 0,
     25656: 0,
     15028: 0,
     14728: 0,
     25683: 0,
     10285: 0,
     712: 0,
     33631: 0,
     21421: 0,
     5046: 0,
     33683: 0,
     720: 0,
     16864: 0,
     721: 0,
     722: 0,
     723: 0,
     724: 0,
     19327: 0,
     17619: 0,
     31045: 0,
     731: 0,
     732: 0,
     28221: 0,
     2258: 0,
     23419: 0,
     26253: 0,
     4392: 0,
     9938: 0,
     10477: 0,
     739: 0,
     29038: 0,
     24295: 0,
     1211: 0,
     6191: 0,
     742: 0,
     35787: 0,
     745: 0,
     17210: 0,
     20628: 0,
     35138: 0,
     11649: 0,
     4015: 0,
     31048: 0,
     5574: 0,
     759: 0,
     29046: 0,
     31011: 0,
     12519: 0,
     761: 0,
     20150: 0,
     762: 0,
     763: 0,
     5794: 0,
     1958: 0,
     5388: 0,
     18488: 0,
     30707: 0,
     6196: 0,
     775: 0,
     7319: 0,
     778: 0,
     779: 0,
     12577: 0,
     781: 0,
     18808: 0,
     3150: 0,
     784: 0,
     785: 0,
     786: 0,
     792: 0,
     793: 0,
     794: 0,
     795: 0,
     796: 0,
     10741: 0,
     6175: 0,
     23861: 0,
     22378: 0,
     19526: 0,
     4428: 0,
     800: 0,
     35058: 0,
     8899: 0,
     6208: 0,
     807: 0,
     20842: 0,
     810: 0,
     1453: 0,
     26368: 0,
     16618: 0,
     18398: 0,
     8612: 0,
     2667: 0,
     18046: 0,
     27702: 0,
     3399: 0,
     18030: 0,
     7669: 0,
     4802: 0,
     815: 0,
     31058: 0,
     18496: 0,
     21256: 0,
     5279: 0,
     2085: 0,
     824: 0,
     3142: 0,
     826: 0,
     32913: 0,
     26336: 0,
     22701: 0,
     4133: 0,
     838: 0,
     839: 0,
     840: 0,
     5860: 0,
     843: 0,
     34661: 0,
     844: 0,
     5001: 0,
     847: 0,
     849: 0,
     12773: 0,
     851: 0,
     20681: 0,
     853: 0,
     854: 0,
     6207: 0,
     33115: 0,
     27115: 0,
     27628: 0,
     13360: 0,
     10732: 0,
     5777: 0,
     863: 0,
     866: 0,
     868: 0,
     21345: 0,
     37361: 0,
     26021: 0,
     31070: 0,
     872: 0,
     873: 0,
     31071: 0,
     876: 0,
     877: 0,
     878: 0,
     24018: 0,
     880: 0,
     882: 0,
     883: 0,
     10014: 0,
     34674: 0,
     887: 0,
     10611: 0,
     890: 0,
     15898: 0,
     6618: 0,
     6601: 0,
     19026: 0,
     16715: 0,
     11644: 0,
     15640: 0,
     34023: 0,
     17797: 0,
     19090: 0,
     25470: 0,
     11657: 0,
     21452: 0,
     29582: 0,
     4909: 0,
     17582: 0,
     2772: 0,
     10724: 0,
     22807: 0,
     16540: 0,
     27046: 0,
     35124: 0,
     37325: 0,
     32297: 0,
     1201: 0,
     22802: 0,
     21106: 0,
     903: 0,
     4332: 0,
     32853: 0,
     908: 0,
     6216: 0,
     911: 0,
     914: 0,
     6880: 0,
     916: 0,
     917: 0,
     37404: 0,
     36349: 0,
     3100: 0,
     924: 0,
     16890: 0,
     33120: 0,
     926: 0,
     27293: 0,
     21491: 0,
     3090: 0,
     935: 0,
     7420: 0,
     2264: 0,
     32973: 0,
     10767: 0,
     32108: 0,
     938: 0,
     939: 0,
     941: 0,
     944: 0,
     33634: 0,
     31082: 0,
     9414: 0,
     954: 0,
     955: 0,
     1675: 0,
     25492: 0,
     957: 0,
     25333: 0,
     959: 0,
     33187: 0,
     7017: 0,
     8156: 0,
     27788: 0,
     969: 0,
     11641: 0,
     970: 0,
     5477: 0,
     28125: 0,
     36900: 0,
     20118: 0,
     30874: 0,
     35337: 0,
     9909: 0,
     17714: 0,
     25568: 0,
     11751: 0,
     15230: 0,
     8867: 0,
     35406: 0,
     30526: 0,
     30887: 0,
     15092: 0,
     12532: 0,
     34461: 0,
     21707: 0,
     5343: 0,
     976: 0,
     978: 0,
     979: 0,
     980: 0,
     982: 0,
     3717: 0,
     7895: 0,
     21562: 0,
     3619: 0,
     984: 0,
     985: 0,
     25838: 0,
     30349: 0,
     34816: 0,
     991: 0,
     992: 0,
     18788: 0,
     27642: 0,
     7256: 0,
     998: 0,
     999: 0,
     11837: 0,
     28717: 0,
     27014: 0,
     12710: 0,
     12258: 0,
     27624: 0,
     6231: 0,
     34266: 0,
     24967: 0,
     1007: 0,
     1010: 0,
     20328: 0,
     9519: 0,
     28011: 0,
     1012: 0,
     35164: 0,
     32019: 0,
     20717: 0,
     15040: 0,
     17575: 0,
     18686: 0,
     8184: 0,
     16141: 0,
     24335: 0,
     28998: 0,
     36517: 0,
     12757: 0,
     1027: 0,
     1028: 0,
     36714: 0,
     33157: 0,
     10405: 0,
     20845: 0,
     36416: 0,
     17554: 0,
     34104: 0,
     10339: 0,
     18706: 0,
     31094: 0,
     33975: 0,
     18757: 0,
     18239: 0,
     26313: 0,
     18628: 0,
     1033: 0,
     2149: 0,
     1036: 0,
     5864: 0,
     27364: 0,
     20844: 0,
     1040: 0,
     10630: 0,
     28454: 0,
     17708: 0,
     1046: 0,
     1047: 0,
     21160: 0,
     15009: 0,
     2727: 0,
     16214: 0,
     16968: 0,
     1056: 0,
     1060: 0,
     16835: 0,
     1061: 0,
     21227: 0,
     36516: 0,
     1065: 0,
     25629: 0,
     28688: 0,
     3531: 0,
     5669: 0,
     1074: 0,
     9475: 0,
     11639: 0,
     37313: 0,
     18428: 0,
     24800: 0,
     1076: 0,
     17346: 0,
     16874: 0,
     11030: 0,
     33130: 0,
     10793: 0,
     1079: 0,
     18943: 0,
     14977: 0,
     34008: 0,
     31108: 0,
     1081: 0,
     1082: 0,
     31334: 0,
     8133: 0,
     6572: 0,
     5761: 0,
     7301: 0,
     9423: 0,
     6169: 0,
     10368: 0,
     34910: 0,
     8189: 0,
     16054: 0,
     28600: 0,
     25042: 0,
     27210: 0,
     26002: 0,
     1086: 0,
     1087: 0,
     1088: 0,
     9400: 0,
     16777: 0,
     33455: 0,
     13958: 0,
     7764: 0,
     ...}



Global Clustering with count zeroes (default)


```python
global_cluster = nx.average_clustering(followers, count_zeros=True)
global_cluster
```




    0.16753704480107323



eccentricity (shortest path with maximum number of nodes)


```python
# import pickle
# with open('eccentricity.pkl', 'rb') as f:
#     eccentricity = pickle.load(f)

eccentricity = nx.eccentricity(followers)
sorted_eccentricity = {k: v for k, v in sorted(eccentricity.items(), key=lambda item: item[1])}

sorted_eccentricity = list(dict(sorted(eccentricity.items(), key=lambda item: item[1], reverse=True)).items())

# get index (node number) and value (node eccentricity value) top 10 after sorting
sorted_eccentricity_indexes = [x[0] for x in sorted_eccentricity]
sorted_eccentricity_values = [x[1] for x in sorted_eccentricity]

# Creating dataframe
top_sorted_eccentricity = pd.DataFrame({'Name':users.iloc[sorted_eccentricity_indexes].name.tolist(), 
                                      'Eccentricity': sorted_eccentricity_values, 
                                      'ml_target':users.iloc[sorted_eccentricity_indexes].ml_target.tolist()})

top_sorted_eccentricity.groupby('Eccentricity').count()['ml_target'].sort_values(ascending=False)
# top_sorted_eccentricity
```




    Eccentricity
    7     27399
    8      8677
    6      1113
    9       480
    10       27
    11        4
    Name: ml_target, dtype: int64



Radius of Followers Graph


```python
radius_of_graph = nx.radius(followers)
radius_of_graph
```

    6
    

Diameter of Followers Graph


```python
diameter_of_graph = nx.diameter(followers)
diameter_of_graph
```

    11
    

For verification diameter=maximum eccentricity

Density of follower


```python
density_of_graph = nx.density(followers)
density_of_graph
```


    0.0004066878203117068


Degree Distribution upto degree value 50 


```python
degree_distrubution = nx.degree_histogram(followers)
fig = plt.figure(figsize=(15, 10))
x = [i for i in range(0, 50)]
plt.bar(x, degree_distrubution[0:50])
plt.show()
```


    
![png](GitHub%20Social%20Network%20Code%20File_files/GitHub%20Social%20Network%20Code%20File_21_0.png)
    


Connected Components


```python
print(nx.is_connected(followers))
print(nx.number_connected_components(followers))
```

    True
    1
    

Average Path Length


```python
average_short_path_length = nx.average_shortest_path_length(followers)
average_short_path_length
```


    3.2464090056353823


_______________


```python
# Creating dataframe
single_value_calc = pd.DataFrame({'Radius': [radius_of_graph], 'Diameter': [diameter_of_graph], 'Density':[density_of_graph], 
                                  'Connected Component': [nx.number_connected_components(followers)],
                                  'Average Path Length': [average_short_path_length]})

# single_value_calc = pd.DataFrame({'Radius': [6], 'Diameter': [11],  'Density': [0.0004066878203117068], 
#                                   'Connected Component': [1], 'Average Path Length': [3.2464090056353823]})

single_value_calc.rename(index={0:'Overall Graph Measures'})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Radius</th>
      <th>Diameter</th>
      <th>Density</th>
      <th>Connected Component</th>
      <th>Average Path Length</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Overall Graph Measures</th>
      <td>6</td>
      <td>11</td>
      <td>0.000407</td>
      <td>1</td>
      <td>3.246409</td>
    </tr>
  </tbody>
</table>
</div>




```python
local_clustering_sort = list((k,v) for k, v in sorted(local_cluster.items(), key=lambda item: item[0], reverse=True))
eccentricity_sort = list((k,v)for k, v in sorted(eccentricity.items(), key=lambda item: item[0], reverse=True))

# get index (node number) and value (node centrality value) top 10 after sorting
sorted_indexes = [x[0] for x in local_clustering_sort]
local_values_sort = [x[1] for x in local_clustering_sort]
eccentricity_values_sort = [x[1] for x in eccentricity_sort]

# Creating dataframe
eccentricity_and_local_cluster = pd.DataFrame({'Name':users.iloc[sorted_indexes].name.tolist(), 
                                      'Eccentricity': eccentricity_values_sort, 
                                      'Local Clustering': local_values_sort})

eccentricity_and_local_cluster
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Eccentricity</th>
      <th>Local Clustering</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>caseycavanagh</td>
      <td>7</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Injabie3</td>
      <td>8</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>qpautrat</td>
      <td>7</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>kris-ipeh</td>
      <td>7</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>shawnwanderson</td>
      <td>8</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>37695</th>
      <td>sunilangadi2</td>
      <td>8</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>37696</th>
      <td>SuhwanCha</td>
      <td>7</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>37697</th>
      <td>JpMCarrilho</td>
      <td>8</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>37698</th>
      <td>shawflying</td>
      <td>8</td>
      <td>0.178571</td>
    </tr>
    <tr>
      <th>37699</th>
      <td>Eiryyy</td>
      <td>8</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>37700 rows × 3 columns</p>
</div>



___________

### Centrality Measures

Degree Centrality


```python
# Applying degree centrality in NetworX
deg_centrality = nx.degree_centrality(followers)

# Applying degree centrality in NetworX
deg_centrality = nx.degree_centrality(followers)
# Sorting degree centrality and getting top 10
sorted_deg_centrality = list(dict(sorted(deg_centrality.items(), key=lambda item: item[1], reverse=True)).items())

# get index (node number) and value (node centrality value) top 10 after sorting
sorted_deg_centrality_indexes = [x[0] for x in sorted_deg_centrality]
sorted_deg_centrality_values = [x[1] for x in sorted_deg_centrality]

# Creating dataframe
top_degree_centrality = pd.DataFrame({'Name':users.iloc[sorted_deg_centrality_indexes].name.tolist(), 
                                      'Degree Centrality': sorted_deg_centrality_values, 
                                      'ml_target':users.iloc[sorted_deg_centrality_indexes].ml_target.tolist()})

top_degree_centrality
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Degree Centrality</th>
      <th>ml_target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dalinhuang99</td>
      <td>0.250882</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>nfultz</td>
      <td>0.187936</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>addyosmani</td>
      <td>0.088172</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bunlong</td>
      <td>0.078464</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>gabrielpconceicao</td>
      <td>0.065466</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>37695</th>
      <td>chrisryancarter</td>
      <td>0.000027</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37696</th>
      <td>kcakdemir</td>
      <td>0.000027</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37697</th>
      <td>chadmazilly</td>
      <td>0.000027</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37698</th>
      <td>orionblastar</td>
      <td>0.000027</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37699</th>
      <td>jovanidash21</td>
      <td>0.000027</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>37700 rows × 3 columns</p>
</div>



Closeness Centrality


```python
# Loading save json of closeness centrality output
# import pickle
# with open('closness_centrality.pkl', 'rb') as f:
#     closeness_centrality = pickle.load(f)

# Applying closeness centrality in NetworX
closeness_centrality = nx.closeness_centrality(followers)


# Sorting degree centrality and getting top 10
sorted_closness_centrality = list(dict(sorted(closeness_centrality.items(), key=lambda item: item[1], reverse=True)).items())

# get index (node number) and value (node centrality value) top 10 after sorting
sorted_closeness_centrality_indexes = [x[0] for x in sorted_closness_centrality]
sorted_closeness_centrality_values = [x[1] for x in sorted_closness_centrality]

# Creating dataframe
top_closeness_centrality = pd.DataFrame({'Name':users.iloc[sorted_closeness_centrality_indexes].name.tolist(), 
                                      'Closeness Centrality': sorted_closeness_centrality_values, 
                                      'ml_target':users.iloc[sorted_closeness_centrality_indexes].ml_target.tolist()})

top_closeness_centrality
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Closeness Centrality</th>
      <th>ml_target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>nfultz</td>
      <td>0.523081</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>dalinhuang99</td>
      <td>0.517787</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bunlong</td>
      <td>0.466324</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>addyosmani</td>
      <td>0.450342</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>gabrielpconceicao</td>
      <td>0.447461</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>37695</th>
      <td>haochenli</td>
      <td>0.155371</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37696</th>
      <td>abhishekpopli</td>
      <td>0.153934</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37697</th>
      <td>scandeiro</td>
      <td>0.147439</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37698</th>
      <td>jazzchipc</td>
      <td>0.145151</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37699</th>
      <td>SOUMAJYOTI</td>
      <td>0.141389</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>37700 rows × 3 columns</p>
</div>



Betweenness Centrality


```python
# Loading save json of closeness centrality output
# import pickle
# with open('betweeness_centrality.pkl', 'rb') as f:
#     betweeness_centrality = pickle.load(f)

# Applying betweeness centrality in NetworX
betweeness_centrality = nx.betweenness_centrality(followers)

# Sorting degree centrality and getting top 10
sorted_between_centrality = list(dict(sorted(betweeness_centrality.items(), key=lambda item: item[1], reverse=True)).items())

# get index (node number) and value (node centrality value) top 10 after sorting
sorted_between_centrality_indexes = [x[0] for x in sorted_between_centrality]
sorted_between_centrality_values = [x[1] for x in sorted_between_centrality]

# Creating dataframe
top_between_centrality = pd.DataFrame({'Name':users.iloc[sorted_between_centrality_indexes].name.tolist(), 
                                      'Betweeness Centrality': sorted_between_centrality_values, 
                                      'ml_target':users.iloc[sorted_between_centrality_indexes].ml_target.tolist()})

top_between_centrality
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Betweeness Centrality</th>
      <th>ml_target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dalinhuang99</td>
      <td>0.269599</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>nfultz</td>
      <td>0.240541</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bunlong</td>
      <td>0.055323</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>addyosmani</td>
      <td>0.043408</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>gabrielpconceicao</td>
      <td>0.035337</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>37695</th>
      <td>chrisryancarter</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37696</th>
      <td>kcakdemir</td>
      <td>0.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37697</th>
      <td>chadmazilly</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37698</th>
      <td>orionblastar</td>
      <td>0.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37699</th>
      <td>jovanidash21</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>37700 rows × 3 columns</p>
</div>




```python
plt.subplot(1,3,1)
plt.xlabel('Centrality Values')
plt.title('Degree Centrality')

top_degree_centrality['Degree Centrality'].plot.hist(figsize=(30, 5), ylim=(0,200))
plt.subplot(1,3,2)
plt.xlabel('Centrality Values')
plt.title('Closeness Centrality')

top_closeness_centrality['Closeness Centrality'].plot.hist(figsize=(30, 5))

plt.subplot(1,3,3)
plt.xlabel('Centrality Values')
plt.title('Betweeness Centrality')

top_between_centrality['Betweeness Centrality'].plot.hist(figsize=(30, 5))

plt.show()

```


    
![png](GitHub%20Social%20Network%20Code%20File_files/GitHub%20Social%20Network%20Code%20File_37_0.png)
    


Visualizing Highest Degree Centrality Node in Graph


```python
followers_network = pd.read_csv('musae_git_edges.csv')
users = pd.read_csv('musae_git_target.csv')

nodes_with_deg_gret_100 = dict((k, v) for k, v in dict(followers.degree).items() if v > 50)

# Creating a function to check if id_1 or id_2 is ML or Web developer
def check_if_exist(id):
    if id in list(nodes_with_deg_gret_100.keys()):
        return 1
    else:
        return 0

followers_network['first_id'] = followers_network['id_1'].apply(check_if_exist)
# followers_network['second_id'] = followers_network['id_2'].apply(check_if_exist)
followers_test = followers_network[(followers_network['first_id'] == 1) & (followers_network['id_2'] == 31890)]
G = nx.from_pandas_edgelist(followers_test, 'id_1', 'id_2')

# Visualizing the highest degree centrality node regin in Graph
fig = plt.figure(figsize=(10, 10))
plt.margins(0,0)

nodes_sizes = []
nodes_color = []

for each in list(G.nodes):
    if each == sorted_deg_centrality[0][0]:
        nodes_sizes.append(4000)
        nodes_color.append('#f02b79')

    elif each == sorted_deg_centrality[1][0]:
        nodes_sizes.append(1000)
        nodes_color.append('#f02b79')
    else:
        nodes_sizes.append(20)
        nodes_color.append('#02A4DE')

print('Highest Degree Centrality Node Lies in Red Shaded Region')
nx.draw(G, node_size=nodes_sizes, node_color=nodes_color, edge_color='#dce8e0')
```

    Highest Degree Centrality Node Lies in Red Shaded Region
    


    
![png](GitHub%20Social%20Network%20Code%20File_files/GitHub%20Social%20Network%20Code%20File_39_1.png)
    


Visualizing Two Highest Closeness Centrality Node in Graph


```python
followers_network = pd.read_csv('musae_git_edges.csv')
users = pd.read_csv('musae_git_target.csv')

nodes_with_deg_gret_100 = dict((k, v) for k, v in dict(followers.degree).items() if v > 50)

# Creating a function to check if id_1 or id_2 is ML or Web developer
def check_if_exist(id):
    if id in list(nodes_with_deg_gret_100.keys()):
        return 1
    else:
        return 0

followers_network['first_id'] = followers_network['id_1'].apply(check_if_exist)
# followers_network['second_id'] = followers_network['id_2'].apply(check_if_exist)
followers_test = followers_network[(followers_network['first_id'] == 1) & (followers_network['id_2'] == 31890)]
G = nx.from_pandas_edgelist(followers_test, 'id_1', 'id_2')

# Visualizing the highest degree centrality node regin in Graph
fig = plt.figure(figsize=(10, 10))
plt.margins(0,0)

nodes_sizes = []
nodes_color = []

for each in list(G.nodes):
    if each == sorted_closness_centrality[0][0]:
        nodes_sizes.append(4000)
        nodes_color.append('#f02b79')

    elif each == sorted_closness_centrality[1][0]:
        nodes_sizes.append(1000)
        nodes_color.append('#f02b79')
    else:
        nodes_sizes.append(20)
        nodes_color.append('#02A4DE')


print('Highest Closeness Centrality Node Lies in Red Shaded Region')
nx.draw(G, node_size=nodes_sizes, node_color=nodes_color, edge_color='#dce8e0')
```

    Highest Closeness Centrality Node Lies in Red Shaded Region
    


    
![png](GitHub%20Social%20Network%20Code%20File_files/GitHub%20Social%20Network%20Code%20File_41_1.png)
    


Visualizing Two Betwenness Closeness Centrality Node in Graph


```python
followers_network = pd.read_csv('musae_git_edges.csv')
users = pd.read_csv('musae_git_target.csv')

nodes_with_deg_gret_100 = dict((k, v) for k, v in dict(followers.degree).items() if v > 50)

# Creating a function to check if id_1 or id_2 is ML or Web developer
def check_if_exist(id):
    if id in list(nodes_with_deg_gret_100.keys()):
        return 1
    else:
        return 0

followers_network['first_id'] = followers_network['id_1'].apply(check_if_exist)
# followers_network['second_id'] = followers_network['id_2'].apply(check_if_exist)
followers_test = followers_network[(followers_network['first_id'] == 1) & (followers_network['id_2'] == 31890)]
G = nx.from_pandas_edgelist(followers_test, 'id_1', 'id_2')

# Visualizing the highest degree centrality node regin in Graph
fig = plt.figure(figsize=(10, 10))
plt.margins(0,0)

nodes_sizes = []
nodes_color = []

for each in list(G.nodes):
    if each == sorted_between_centrality[0][0]:
        nodes_sizes.append(4000)
        nodes_color.append('#f02b79')

    elif each == sorted_between_centrality[1][0]:
        nodes_sizes.append(1000)
        nodes_color.append('#f02b79')
    else:
        nodes_sizes.append(20)
        nodes_color.append('#02A4DE')


print('Highest Betweenness Centrality Node Lies in Red Shaded Region')
nx.draw(G, node_size=nodes_sizes, node_color=nodes_color, edge_color='#dce8e0')
```

    Highest Betweenness Centrality Node Lies in Red Shaded Region
    


    
![png](GitHub%20Social%20Network%20Code%20File_files/GitHub%20Social%20Network%20Code%20File_43_1.png)
    

