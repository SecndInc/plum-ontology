# Lead

Mirror table `sf_lead_runs` · 176 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Lead ID |
| IsDeleted | boolean | 100% | Deleted · false (176) |
| Title | string | 81% |  |
| Company | string | 100% |  |
| City | string | 4% |  |
| State | string | 4% | State/Province |
| Country | string | 18% |  |
| Website | url | 7% |  |
| LeadSource | picklist | 85% | Lead Source · Referral - Team (117), (blank) (26), Referral - Partner (23), Website (5), Other (2), Trade Show (1), Employee Referral (1), Advertisement (1) |
| Status | picklist | 100% | New Lead (96), Qualified (46), New (30), Working (2), Nurturing (1), Internal Debrief (1) |
| Industry | picklist | 66% | (blank) (59), Retail (27), Technology (17), Media (17), Finance (17), Hospitality (9), Healthcare (6), Manufacturing (4), Food & Beverage (4), Apparel (4) |
| Rating | picklist | 65% | (blank) (61), Warm (60), Cold (43), Hot (12) |
| CurrencyIsoCode | picklist | 100% | Lead Currency · USD (100), CAD (76) |
| NumberOfEmployees | int | 3% | Employees · 124 … 8500 |
| OwnerId | reference | 100% | Owner ID · → Group, User |
| IsConverted | boolean | 100% | Converted · false (130), true (46) |
| ConvertedDate | date | 26% | Converted Date · 2025-03-26 … 2026-09-17 |
| ConvertedAccountId | reference | 24% | Converted Account ID · → Account |
| ConvertedContactId | reference | 24% | Converted Contact ID · → Contact |
| ConvertedOpportunityId | reference | 22% | Converted Opportunity ID · → Opportunity |
| IsUnreadByOwner | boolean | 100% | Unread By Owner · true (116), false (60) |
| CreatedDate | datetime | 100% | Created Date · 2025-01-20 05:42:53 … 2026-09-17 16:04:46 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-01-20 05:42:53 … 2026-09-17 20:07:07 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-01-23 14:11:26 … 2026-09-24 21:51:12 |
| LastActivityDate | date | 2% | Last Activity · 2025-02-01 … 2025-11-10 |
| IsPriorityRecord | boolean | 100% | Important · false (176) |

Never filled: MasterRecordId, LastViewedDate, LastReferencedDate, Jigsaw, JigsawContactId, EmailBouncedReason, EmailBouncedDate.

Bulk creation days: 2026-09-01 (100).
