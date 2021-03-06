File analysis of the codeplug data file used by CPS v2.0.5 with firmware 3.0.6

The codeplug (.dat) file used by the Radioddity CPS (PC exe software used to manage the transceiver settings e.g. channels, contacts etc ) is a binary file, 128k bytes long.

The format of this file seems to be different based on both the CPS version and the firmware version in the transceiver.

This data is for firmware version 3.0.6, but other firmware versions are know to have a different structure.

The file consists of multiple fixed length, fixed position data blocks. These data blocks contain things like the Contacts, the Channels, the Zones, the Scan lists, the Rx Group lists, as well as the "Boot Item", and "Basic information" settings.

As this file seems to vary in format between different versions of the CPS, and because the CPS is matched to each firmware version (though the version numbers don't tally), I think its likely that this binary file is uploaded straight into the transcreiver with little modification by the CPS.
This has been partially confirmed, because I updated the firmware in my transceiver, and read back the codeplug, and the resultant data file, has remnants from the previos data mixed in with the new data. In this case there appears to be areas of redundant data in the file, or possibly the old data has not been fully overwritten by new data, as I don't have the maximum number of Channels or Contacts etc defined in the codeplug.


# Data formats within the file

Text strings seem to be in single byte ASCII. Terminated by 0xff. All unused text bytes seem to be filled with 0xff

Numerical values e.g. frequencies and other numbers seem to be stored in a sort of BCD with 2 decimal digits per byte.
e.g. the number 520 woudl be encoded into 2 bytes as 0x20 0x05
Sometimes the digits are not transposed, e.g. a numerical password of 123456 is encoded as  0x12 0x34 0x56


#Default file

Initially when the CPS starts, it loads Default.dat from the same folder that the CPS (DMR.exe) is located.

When this 'default' file is resaved, the CPS seems to update the default to include version information about the CPS and also the original filename form which it was created.

00001470: 32 19 06 01 01 03 80 00 - BE 9C 4B CE AA 2D 4C 73 |2         K  -Ls|
00001480: 17 2A 00 00 00 A2 BA 1A - 00 00 00 02 00 00 00 00 | *              |
00001490: 00 00 00 00 00 00 00 00 - 00 00 00 47 00 44 00 2D |           G D -|
000014a0: 00 37 00 37 00 20 00 76 - 00 32 00 2E 00 30 00 2E | 7 7   v 2 . 0 .|
000014b0: 00 35 00 00 00 1A 00 4A - 00 31 00 00 00 00 00 2D | 5     J 1     -|
000014c0: 4C 09 17 10 00 44 41 54 - 41 00 00 36 00 08 00 04 |L    DATA  6    |
000014d0: 00 EF BE 9C 4B CE AA 2D - 4C 09 17 2A 00 00 00 A3 |    K  -L  *    |
000014e0: BA 1A 00 00 00 02 00 00 - 00 00 00 00 00 00 00 00 |                |
000014f0: 00 00 00 00 00 44 00 41 - 00 54 00 41 00 00 00 14 |     D A T A    |
00001500: 00 5E 00 32 00 00 00 02 - 00 2D 4C FC 15 20 00 44 | ^ 2     -L    D|
00001510: 65 66 61 75 6C 74 2E 64 - 61 74 00 44 00 08 00 04 |efault.dat D    |
00001520: 00 EF BE 2D 4C FC 15 2D - 4C FC 15 2A 00 00 00 B4 |   -L  -L  *    |
00001530: EA 1A 00 00 00 15 00 00 - 00 00 00 00 00 00 00 00 |                |
00001540: 00 00 00 00 00 44 00 65 - 00 66 00 61 00 75 00 6C |     D e f a u l|
00001550: 00 74 00 2E 00 64 00 61 - 00 74 00 00 00 1A 00 00 | t . d a t      |
00001560: 00 4E 3D 0B 60 36 2A 0B - A8 33 2A 0B 78 36 2A 0B | N= `6*  3* x6* |

Specifically the bytes from 0x1478 onwards are updated. Strangely, if the file is resaved again, often the CPS seems to erase this block back to

00001470: 32 19 06 01 01 03 80 00 - 00 00 00 00 00 00 00 00 |2               |
00001480: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
00001490: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
000014a0: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
000014b0: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
000014c0: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
000014d0: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
000014e0: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
000014f0: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
00001500: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
00001510: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
00001520: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
00001530: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
00001540: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
00001550: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
00001560: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |

This block sometimes contains data like this

00001470: 32 19 06 01 01 03 80 00 - 22 00 6E 00 6F 00 6E 00 |2       " n o n |
00001480: 65 00 22 00 2F 00 3E 00 - 0D 00 0A 00 3C 00 2F 00 |e " / >     < / |
00001490: 54 00 65 00 6D 00 70 00 - 6C 00 61 00 74 00 65 00 |T e m p l a t e |
000014a0: 42 00 61 00 63 00 6B 00 - 67 00 72 00 6F 00 75 00 |B a c k g r o u |
000014b0: 6E 00 64 00 3E 00 0D 00 - 0A 00 3C 00 53 00 69 00 |n d >     < S i |
000014c0: 7A 00 65 00 72 00 20 00 - 69 00 64 00 3D 00 22 00 |z e r   i d = " |
000014d0: 61 00 74 00 6F 00 6D 00 - 28 00 52 00 65 00 61 00 |a t o m ( R e a |
000014e0: 64 00 69 00 6E 00 67 00 - 50 00 61 00 6E 00 65 00 |d i n g P a n e |
000014f0: 53 00 69 00 7A 00 65 00 - 72 00 29 00 22 00 20 00 |S i z e r ) "   |
00001500: 73 00 69 00 7A 00 69 00 - 6E 00 67 00 74 00 61 00 |s i z i n g t a |
00001510: 72 00 67 00 65 00 74 00 - 3D 00 22 00 61 00 74 00 |r g e t = " a t |
00001520: 6F 00 6D 00 28 00 52 00 - 65 00 61 00 64 00 69 00 |o m ( R e a d i |
00001530: 6E 00 67 00 50 00 61 00 - 6E 00 65 00 29 00 22 00 |n g P a n e ) " |
00001540: 20 00 47 00 72 00 6F 00 - 77 00 54 00 61 00 72 00 |  G r o w T a r |
00001550: 67 00 65 00 74 00 46 00 - 69 00 72 00 73 00 74 00 |g e t F i r s t |
00001560: 3D 00 22 00 74 00 72 00 - 75 00 65 00 22 00 20 00 |= " t r u e "   |

IMHO. It looks lika bug / memory leak, where something is overwriting the copy of the codeplug held in memory

#Basic information (screen)

The only editable items on this page are the frequency range. 

This data represents

UHF range frequency from 401 - 520Mhz, and VHF frequency range 137 - 520Mhz

00000080: 01 04 20 05 37 01 74 01   

Note. Normally 520Mhz can't been selected in the CPS, but I have modified my CPS to allow extended ranges to be entered.
This will be documented in another file relating to the CPS its self


#Boot item (screen)

The Boot Item data is held here

Password data is in bytes 0x7519 to 0x751E
Password enable is in 0x7159 , 0x00 = disabled 0x01 = enabled
Password number is in bytes 0x751B - 0x751E

00007510: FF FF FF FF FF FF FF FF - 01 01 00 00 12 34 56 00 |             4V |

e.g. The 0x01 at address 00007519 indicates that password protection is enabled, with password is set to 123456


00007540: 42 6F 6F 74 20 4C 69 6E - 65 20 31 FF FF FF FF FF |Boot Line 1     |
00007550: 42 6F 6F 74 20 4C 69 6E - 65 20 32 FF FF FF FF FF |Boot Line 2     |

Text for Line 1 and Line 2 can be seen at 0x7540 and 0x7550

#Menu (screen)

I have not looked for this data yet


#Number Key Assign (screen)

No keys assigned data is

00007520: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
00007530: 00 00 00 00 00 00 00 00 - 0A FF FF FF 07 00 84 70 |               p|

Assigned
Number key 0: Contact 1
Number key 1: Contact 2
Number key 2: Contact 3
Number key 3: Contact 1
Number key 4: Contact 2
Number key 5: Contact 3
Number key 6: Contact 1
Number key 7: Contact 2
Number key 8: Contact 3
Number key 9: Contact 1

Yields this data

00007520: FF 03 00 00 01 00 02 00 - 03 00 01 00 02 00 03 00 |                |
00007530: 01 00 02 00 03 00 01 00 - 0A FF FF FF 07 00 84 70 |               p|

It looks like the data for Number Key 0 starts at 0x7524 (for 2 bytes, low byte first). 
Precise encoding of the Contact numbers is not known at the moment.

#General settings (screen)

Radio name and Radio IDare stored at 0x000e0

000000e0: 52 41 44 49 4F 5F 4E 41 - 12 34 56 78 00 00 00 00 |RADIO_NA 4Vx    |

Radio name is max of 8 characters, ID is stored as decimal in each nibble 
The number entered in this case was 12345678

This screen contains other data which needs to be analysed and documented.

#Buttons (screen)

Data appears to be in address 0x108 to 0x10F

Setting for Long Press duration (ms) 1750
Menus increasing in item number e.g SK1 (short) first menu, SK1 (long) second menu etc

00000100: FF FF FF FF FF FF FF FF - 01 07 00 01 02 03 04 05 |  

Hence it looks like 0x10A is SK1 (short) with 0x00 = first menu option

Address 0x109 contains the "Long Press Durarion". Although this appears to be a enterable number, its actually a list where 1750 is the third option.
When 1500 ms is selected byte 0x10A is 0x06. So the minimum number value is 0x04 for 1000ms 

#Text Message (screen)

Max length 144 characters


First text message store at 0x170

00000170: 4C 6F 72 65 6D 20 69 70 - 73 75 6D 20 64 6F 6C 6F |Lorem ipsum dolo|
00000180: 72 20 73 69 74 20 61 6D - 65 74 2C 20 63 6F 6E 73 |r sit amet, cons|
00000190: 65 63 74 65 74 75 72 20 - 61 64 69 70 69 73 63 69 |ectetur adipisci|
000001a0: 6E 67 20 65 6C 69 74 2E - 20 45 74 69 61 6D 20 74 |ng elit. Etiam t|
000001b0: 69 6E 63 69 64 75 6E 74 - 2C 20 6C 6F 72 65 6D 20 |incidunt, lorem |
000001c0: 61 63 20 73 6F 6C 6C 69 - 63 69 74 75 64 69 6E 20 |ac sollicitudin |
000001d0: 6D 61 78 69 6D 75 73 2C - 20 76 65 6C 69 74 20 61 |maximus, velit a|
000001e0: 75 67 75 65 20 73 61 67 - 69 74 74 69 73 20 73 65 |ugue sagittis se|
000001f0: 6D 2C 20 62 6C 61 6E 64 - 69 74 20 62 6C 61 6E 64 |m, blandit bland|

Second text message stored at 0x200

00000200: 4E 61 6D 20 73 65 64 20 - 70 6F 72 74 74 69 74 6F |Nam sed porttito|
00000210: 72 20 6D 69 2E 20 43 72 - 61 73 20 73 65 64 20 6C |r mi. Cras sed l|
00000220: 69 62 65 72 6F 20 61 63 - 20 6C 6F 72 65 6D 20 70 |ibero ac lorem p|
00000230: 65 6C 6C 65 6E 74 65 73 - 71 75 65 20 73 6F 6C 6C |ellentesque soll|
00000240: 69 63 69 74 75 64 69 6E - 2E 20 41 65 6E 65 61 6E |icitudin. Aenean|
00000250: 20 65 74 20 74 6F 72 74 - 6F 72 20 76 65 6C 20 6E | et tortor vel n|
00000260: 69 73 6C 20 6D 61 74 74 - 69 73 20 66 72 69 6E 67 |isl mattis fring|
00000270: 69 6C 6C 61 2E 20 51 75 - 69 73 71 75 65 20 6E 6F |illa. Quisque no|
00000280: 6E 20 6C 65 6F 20 6E 6F - 6E 20 64 75 69 20 75 6C |n leo non dui ul|

Maximum number of Text messages TBD

#Privacy (screen)

TBD

#Signaling System

DTMF and Emergency System  - TBD

#Contact (section)

DTMF - TBD

#Digital Contact (Screen)

Default data has 3 contacts, as examples of the 3 types of contact

00017620: 43 6F 6E 74 61 63 74 31 - FF FF FF FF FF FF FF FF |Contact1        |
00017630: 00 00 00 01 00 01 00 FF - 43 6F 6E 74 61 63 74 32 |        Contact2|
00017640: FF FF FF FF FF FF FF FF - 00 00 00 01 01 01 00 FF |                |
00017650: 43 6F 6E 74 61 63 74 33 - FF FF FF FF FF FF FF FF |Contact3        |

Renaming Contact1,Contact2 and Contact3 
Changed Contact1, Call ID from 00000001 to 11111111 and
Changed Contact2, Call ID from 00000001 to 12222222 

Yielded
 
00017620: 43 6F 6E 74 61 63 74 31 - 41 FF FF FF FF FF FF FF |Contact1A       |
00017630: 11 11 11 11 00 01 00 FF - 43 6F 6E 74 61 63 74 32 |        Contact2|
00017640: 41 FF FF FF FF FF FF FF - 12 22 22 22 01 01 00 FF |A        """    |
00017650: 43 6F 6E 74 61 63 74 33 - 41 FF FF FF FF FF FF FF |Contact3A       |

Contact record appears to be 24 bytes long.
First 16 bytes are the name, with unused characters filled with 0xff
Call ID is decimal coded in hex (nibbles) from offset 0x10 to 0x13

Offset 0x14 is Contact Type. 
0x00 = "Group All"  (this is supposed to read Group Call)
0x01 = Private call

Offset 0x15 is Call Receive tone enable 0x00 is disable 0x01 is enable
(all the contacts in this example have this enabled)

Offset 0x16 is the "Ring Style" 0x00 = None, 0x01 = 1 etc

Adding a additional contact, changes the data next to the existing data e.g


00017650: 43 6F 6E 74 61 63 74 33 - 41 FF FF FF FF FF FF FF |Contact3A       |
00017660: 16 77 72 15 02 01 00 FF - FF FF FF FF FF FF FF FF | wr             |
00017670: FF FF FF FF FF FF FF FF - FF FF FF FF FF FF FF FF |               |

becomes

00017650: 43 6F 6E 74 61 63 74 33 - 41 FF FF FF FF FF FF FF |Contact3A       |
00017660: 16 77 72 15 02 01 00 FF - 54 47 35 30 35 FF FF FF | wr     TG505   |
00017670: FF FF FF FF FF FF FF FF - 00 00 05 05 00 01 00 FF |                |

When TG5-5 with ID 00000505 is added

Editing the dat file to add another record also worked 


00017680: 43 6F 6E 74 61 63 74 39 - 39 FF FF FF FF FF FF FF |Contact99       |
00017690: 11 11 11 99 00 01 00 FF - FF FF FF FF FF FF FF FF |                |

I also changed the first byte of Contact99 to 0xFF and it was no longer visible in the CPS, which suggests the CPS just looks for 0xff in the first byte of the contacts list.

I added multiple contacts manually, with no apparent problems to the CPS in terms of is Contacts display

However due to the relationship betwen contacts and Channels and RX Group lists, this may be different if they exist




#Rx Group list (screen)

Renaming the group which is already in the default file and adding in the first 16 contacts from the Digital Contacts, and adding a second (empty) Rx Group, changed this 

0001d620: 01 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d630: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d640: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d650: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d660: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d670: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d680: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d690: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d6a0: 47 72 6F 75 70 4C 69 73 - 74 31 FF FF FF FF FF FF |GroupList1      |
0001d6b0: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d6c0: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d6d0: FF FF FF FF FF FF FF FF - FF FF FF FF FF FF FF FF |                |
0001d6e0: FF FF FF FF FF FF FF FF - FF FF FF FF FF FF FF FF |                |
0001d6f0: FF FF FF FF FF FF FF FF - FF FF FF FF FF FF FF FF |  

To this


0001d620: 10 01 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d630: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d640: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d650: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d660: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d670: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d680: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d690: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d6a0: 47 72 6F 75 70 4C 69 73 - 74 41 42 43 44 45 46 FF |GroupListABCDEF |
0001d6b0: 01 00 02 00 03 00 04 00 - 05 00 06 00 07 00 08 00 |                |
0001d6c0: 09 00 0A 00 0B 00 0C 00 - 0D 00 0E 00 0F 00 00 00 |                |
0001d6d0: 47 72 6F 75 70 4C 69 73 - 74 32 FF FF FF FF FF FF |GroupList2      |
0001d6e0: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |
0001d6f0: 00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00 |                |


Adddress 0x0001d620 changed from 01 to 04, when the number of Contacts changed from 0 to 3, hence the addresses from 01d620 onwards hold the Contacts count for the Rx Group list items from address 0x1d6a0 onwards

Maximum groups per list is 15, which is dictated by the storage area allocated for each record

e.g. each record is 48 bytes long

Rx Group Name can be 1 to 15 characters, byte offset 15 always seems to contain the terminator character 0xff 
Data from offset 0x10 to 0x2D hold the list of Contacts in the group, with formatting 
01 00 = Contact 0x0001


#Channels (screen)

Renaming the Channel1 in the default data to Channel1A

changed this

00003790: 43 68 61 6E 6E 65 6C 31 - FF FF FF FF FF FF FF FF |Channel1        |
000037a0: 00 25 40 14 00 25 40 14 - 01 00 00 00 FF 00 50 01 | %@  %@       P |
000037b0: FF FF FF FF 00 00 00 00 - 16 01 00 01 00 01 01 00 |                |
000037c0: 00 00 00 81 00 00 00 00 - 43 68 61 6E 6E 65 6C 32 |        Channel2|
000037d0: FF FF FF FF FF FF FF FF - 00 25 41 14 00 25 41 14 |         %A  %A |
000037e0: 01 00 00 00 FF 00 50 00 - FF FF FF FF 00 00 00 00 |      P         |
000037f0: 16 01 01 01 01 01 00 00 - 00 00 00 81 00 00 00 00 |                |

To this

00003790: 43 68 61 6E 6E 65 6C 31 - 41 FF FF FF FF FF FF FF |Channel1A       |
000037a0: 00 25 40 14 00 25 40 14 - 01 00 00 00 FF 00 50 01 | %@  %@       P |
000037b0: FF FF FF FF 00 00 00 00 - 16 01 00 01 00 01 01 00 |                |
000037c0: 00 00 00 81 00 00 00 00 - 43 68 61 6E 6E 65 6C 32 |        Channel2|
000037d0: FF FF FF FF FF FF FF FF - 00 25 41 14 00 25 41 14 |         %A  %A |
000037e0: 01 00 00 00 FF 00 50 00 - FF FF FF FF 00 00 00 00 |      P         |
000037f0: 16 01 01 01 01 01 00 00 - 00 00 00 81 00 00 00 00 |                |

Channel names can be 1 to 15 characters, terminated with 0xff in the first 16 bytes of the Channel recod
Offset 0x10 - 0x13  bytes 00 25 40 14 is Rx frequency (144.02500)
Offset 0x14 - 0x17  bytes 00 25 40 14 is Tx frequency (144.02500)
Offset 0x18 Mode. 0x00 = Digital 0x01 = Analogue
Offset 0x1B TOT timer 0x00 = infinite 0x01 = 15 secs, 0x02 = 30 secs, max value = 0x21 = 495 secs
Offset 0x1C TOT rekey time 0xFF = 255 seconds (Note, if TOT is infinite this is grayed out in the UI)
Offset 0x1D Admit criteria 0x00 = Always 0x01 = Channel free, 0x02 Colour code (digital mode only)
Offset 0x1F Scan list number 0x00 = None 0x01 = First scan list etc
Offset 0x33 Bit fields 
Bit 0  Squelch  Normal 1 = Tight
Bit 1 Autoscan (1 = enabled)
Bit 3 Power level 0 = Low 1 = High


Other settings TBD






#REST OF FILE TDB


