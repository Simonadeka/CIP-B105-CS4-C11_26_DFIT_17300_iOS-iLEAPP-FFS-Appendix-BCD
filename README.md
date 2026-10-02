# CIP-B105-CS4-C11_26_DFIT_17300_iOS-iLEAPP-FFS-Appendix-BCD

[Forensics](https://img.shields.io/badge/Forensics-iOS_FS-blue) [iLEAPP](https://img.shields.io/badge/iLEAPP-v2026.4.4--dev-green) [Artifacts](https://img.shields.io/badge/Artifacts-1173_Processed-success) [TSV](https://img.shields.io/badge/TSV-304_Validated-orange) [Deliverable](https://img.shields.io/badge/Appendix_BCD-24_Files_6889_Lines_184K-brightgreen)

**FTK Case 304 TSV Validated | 24 Files 6889 Lines 184K Deliverable | 1173 Artifacts**

## Executive Summary
iOS FS image `13-4-1_tar_9.tar (8.6M)` - Preservation `du -sh 17G` with `cp -r` - iLEAPP FS parser 1208 modules **1173/1173** completed - Report 12M + index 456K + lava 212K/222K - 304 TSV total - Filtered 24 files 6889 lines 704K -> 184K zip for Appendix B/C/D.

## Key Findings
| Artefact | Validation | Figure |
| :--- | :--- | :--- |
| Safari History 2.4K | MLB 2020, NHL Resume, COVID 03-2020 | Fig-04_Safari, Fig-07 |
| Call History 4.9K + Group 5.4K/37 | 9197627808 Fuquay-Varina 37 entries | Fig-03_Call, Fig-12 |
| SMS / Preview Cache 1.9K | Threaded view | Fig-07, Fig-10 |
| Contacts 2 | Josh Hickman DFIR ref | Fig-08 |
| WhatsApp 12 entries | ChatStorage 12 | Fig-09 |
| KnowledgeC Battery 283K + DND 158K + AppUsage 76K | Device behavior | Fig-14 |

###  Compliance 
- 48h Chronology: 2020-03-12 to 2020-03-14 - 6 events across Safari/KnowledgeC/Call/SMS/WhatsApp - see Section 6A in report PDF
- Manual Validation: DB Browser for SQLite query validated iLEAPP - see Section 6A
- Corroborated Relationships: Call 9197627808 = SMS + Contact, Safari search = App Usage + Battery

## Methodology
```bash
# 1. Preservation - Task A
df -h; cp -r /media/sf_FTK_Case_File/ ~/Case_Working/; du -sh 17G; ls -lh 13-4-1_tar_9.tar 8.6M

# 2. Processing
python3 ileapp.py -t fs -i .../13-4-1_tar_9.tar -o .../FFS_Report/ # 1173 artifacts

# 3. Verification
firefox .../index.html & # PID 51162
ls -lh .../index.html 456K; .../_lava_artifacts.db 212K; .../_lava_data.lava 222K

# 4. TSV Inventory Fix
find ~/Case_Reports/ -name "*.tsv" | wc -l # 304 total
ls -1 .../_TSV\ Exports/ | grep -iE "sms|call|safari|cal" # 30+ core

# 5. Appendix BCD
mkdir ~/Desktop/Final_Appendix_BCD; cp *SMS* *Call* *Safari* *Knowledge* Final/
cat *.tsv | wc -l # 6889; wc -l # 24; du -sh 704K; zip -r FFS_Appendix_BCD.zip Final/ # 184K
## Deliverable
*FFS_Appendix_BCD.zip - 184K* = 24 files, 6889 lines, 704K uncompressed, deflation 35%-91% validated. Ready for Appendix B/C/D.

## Repository Structure
├── FFS_Appendix_BCD.zip (184K deliverable)
├── Report_Screenshots/ (26 Figures)
│   ├── Figure-00_Command_Execution_FS_Type_1208_Modules
│   ├── Figure-01_Index_Html_Firefox_5116
│   ├── Figure-03_Call_History_9197627808
│   ├── Figure-03_Parser_Completed_1173
│   ├── Figure-04_FS_Report_12M + Figure-04b + Figure-13_Output_Structure
│   ├── Figure-05_TSV_Filtered + Figure-10_Full_304 + Figure-11-06_24_6889
│   ├── Figure-06_Zip + Figure-14_BCD_Creation
│   ├── Figure-15b_Forensic_Preservation_Chain_Custody
│   └── Figure-07_08_09_Safari_SMS_Contacts_WhatsApp
└── Final_Appendix_BCD/ (704K)
    ├── Safari - History/Bookmarks/Cache/Favicons/iCloud/Search
    ├── SMS, Apple SMS Preview Cache, Call History, Group Call
    ├── knowledgeC - AppUsage/Battery/Lock/Plugin/DND/Media
    └── TextNow/Zoom/WhatsApp/tl.db
## Chain of Custody
Source 13-4-1_tar_9.tar 8.6M -> Case_Working 17GB -> FS_Report 12M + FFS_Report 304 TSV -> Final_Appendix_BCD 24/6889/704K -> FFS_Appendix_BCD.zip 184K

## Tools
Kali Linux, iLEAPP v2026.4.4-dev FS Parser, Firefox, FTK Imager

*Author:* Simon Friday Adeka - Digital Forensics - Oct 2026 - Josh Hickman dataset

