# Contact

Mirror table `sf_contact_runs` · 76 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Contact ID |
| IsDeleted | boolean | 100% | Deleted · false (76) |
| AccountId | reference | 97% | Account ID · → Account |
| MailingCity | string | 3% | Mailing City |
| MailingState | string | 3% | Mailing State/Province |
| MailingCountry | string | 3% | Mailing Country |
| ReportsToId | reference | 1% | Reports To ID · → Contact |
| Title | string | 37% |  |
| CurrencyIsoCode | picklist | 100% | Contact Currency · CAD (51), USD (25) |
| OwnerId | reference | 100% | Owner ID · → User |
| CreatedDate | datetime | 100% | Created Date · 2025-03-14 19:52:31 … 2026-09-17 20:07:06 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-03-18 19:18:46 … 2026-09-17 20:07:06 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-03-24 15:39:21 … 2026-09-17 20:07:07 |
| LastActivityDate | date | 12% | Last Activity · 2025-01-10 … 2026-09-16 |
| IsEmailBounced | boolean | 100% | Is Email Bounced · false (76) |
| IsPriorityRecord | boolean | 100% | Important · false (76) |
| TitleType | picklist | 18% | Seniority Level · (blank) (62), vp (5), executive (5), directorOrManager (3), ceo (1) |
| Type__c | picklist | 29% | Type · (blank) (54), Prospect (9), Customer (8), Partner (4), Vendor (1) |

Never filled: MasterRecordId, Department, LastCURequestDate, LastCUUpdateDate, LastViewedDate, LastReferencedDate, EmailBouncedReason, EmailBouncedDate, Jigsaw, JigsawContactId, ContactSource, DepartmentGroup, BuyerAttributes.

Bulk creation days: 2026-07-08 (18).
