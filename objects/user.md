# User

Mirror table `sf_user_runs` · 44 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | User ID |
| CompanyName | string | 16% | Company Name |
| Department | string | 2% |  |
| Title | string | 2% |  |
| Country | string | 11% |  |
| EmailPreferencesAutoBcc | boolean | 100% | AutoBcc · true (44) |
| EmailPreferencesAutoBccStayInTouch | boolean | 100% | AutoBccStayInTouch · false (44) |
| EmailPreferencesStayInTouchReminder | boolean | 100% | StayInTouchReminder · true (44) |
| BadgeText | string | 100% | User Photo badge text overlay |
| IsActive | boolean | 100% | Active · true (30), false (14) |
| TimeZoneSidKey | picklist | 100% | Time Zone · America/New_York (40), America/Los_Angeles (3), America/Vancouver (1) |
| LocaleSidKey | picklist | 100% | Locale · en_CA (39), en_US (5) |
| ReceivesInfoEmails | boolean | 100% | Info Emails · true (41), false (3) |
| ReceivesAdminInfoEmails | boolean | 100% | Admin Info Emails · true (22), false (22) |
| EmailEncodingKey | picklist | 100% | Email Encoding · UTF-8 (44) |
| DefaultCurrencyIsoCode | picklist | 100% | Default Currency ISO Code · CAD (43), USD (1) |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · CAD (38), USD (6) |
| ProfileId | reference | 100% | Profile ID · → Profile |
| UserType | picklist | 100% | User Type · Standard (40), AutomatedProcess (2), CsnOnly (1), CloudIntegrationUser (1) |
| StartDay | picklist | 64% | Start of Day · 6 (27), (blank) (16), 8 (1) |
| EndDay | picklist | 64% | End of Day · 23 (27), (blank) (16), 18 (1) |
| LanguageLocaleKey | picklist | 100% | Language · en_US (44) |
| LastLoginDate | datetime | 59% | Last Login · 2025-02-25 18:52:33 … 2026-09-29 16:25:20 |
| LastPasswordChangeDate | datetime | 59% | Last Password Change or Reset · 2021-02-03 17:13:18 … 2026-09-29 04:07:27 |
| CreatedDate | datetime | 100% | Created Date · 2025-01-20 05:42:53 … 2026-09-28 20:53:21 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-01-20 05:42:53 … 2026-09-29 16:21:36 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-09-21 08:03:06 … 2026-09-29 16:21:36 |
| PasswordExpirationDate | datetime | 70% | Password Expiration Date · 2021-05-04 17:13:18 … 2026-12-28 04:07:27 |
| NumberOfFailedLogins | int | 64% | Failed Login Attempts · 0 … 3 |
| UserPermissionsMarketingUser | boolean | 100% | Marketing User · false (29), true (15) |
| UserPermissionsOfflineUser | boolean | 100% | Offline User · false (44) |
| UserPermissionsAvantgoUser | boolean | 100% | AvantGo User · false (44) |
| UserPermissionsCallCenterAutoLogin | boolean | 100% | Auto-login To Call Center · false (44) |
| UserPermissionsSFContentUser | boolean | 100% | Salesforce CRM Content User · false (44) |
| UserPermissionsKnowledgeUser | boolean | 100% | Knowledge User · false (44) |
| UserPermissionsInteractionUser | boolean | 100% | Flow User · false (32), true (12) |
| UserPermissionsSupportUser | boolean | 100% | Service Cloud User · false (44) |
| ForecastEnabled | boolean | 100% | Allow Forecasting · false (41), true (3) |
| UserPreferencesActivityRemindersPopup | boolean | 100% | ActivityRemindersPopup · true (44) |
| UserPreferencesEventRemindersCheckboxDefault | boolean | 100% | EventRemindersCheckboxDefault · true (44) |
| UserPreferencesTaskRemindersCheckboxDefault | boolean | 100% | TaskRemindersCheckboxDefault · true (44) |
| UserPreferencesReminderSoundOff | boolean | 100% | ReminderSoundOff · false (44) |
| UserPreferencesDisableAllFeedsEmail | boolean | 100% | DisableAllFeedsEmail · false (44) |
| UserPreferencesDisableFollowersEmail | boolean | 100% | DisableFollowersEmail · false (44) |
| UserPreferencesDisableProfilePostEmail | boolean | 100% | DisableProfilePostEmail · false (44) |
| UserPreferencesDisableChangeCommentEmail | boolean | 100% | DisableChangeCommentEmail · false (44) |
| UserPreferencesDisableLaterCommentEmail | boolean | 100% | DisableLaterCommentEmail · false (44) |
| UserPreferencesDisProfPostCommentEmail | boolean | 100% | DisProfPostCommentEmail · false (44) |
| UserPreferencesApexPagesDeveloperMode | boolean | 100% | ApexPagesDeveloperMode · false (44) |
| UserPreferencesReceiveNoNotificationsAsApprover | boolean | 100% | ReceiveNoNotificationsAsApprover · false (44) |
| UserPreferencesReceiveNotificationsAsDelegatedApprover | boolean | 100% | ReceiveNotificationsAsDelegatedApprover · false (44) |
| UserPreferencesHideCSNGetChatterMobileTask | boolean | 100% | HideCSNGetChatterMobileTask · false (44) |
| UserPreferencesDisableMentionsPostEmail | boolean | 100% | DisableMentionsPostEmail · false (44) |
| UserPreferencesDisMentionsCommentEmail | boolean | 100% | DisMentionsCommentEmail · false (44) |
| UserPreferencesHideCSNDesktopTask | boolean | 100% | HideCSNDesktopTask · false (44) |
| UserPreferencesHideChatterOnboardingSplash | boolean | 100% | HideChatterOnboardingSplash · false (44) |
| UserPreferencesHideSecondChatterOnboardingSplash | boolean | 100% | HideSecondChatterOnboardingSplash · false (44) |
| UserPreferencesDisCommentAfterLikeEmail | boolean | 100% | DisCommentAfterLikeEmail · false (44) |
| UserPreferencesDisableLikeEmail | boolean | 100% | DisableLikeEmail · true (39), false (5) |
| UserPreferencesSortFeedByComment | boolean | 100% | SortFeedByComment · true (39), false (5) |
| UserPreferencesDisableMessageEmail | boolean | 100% | DisableMessageEmail · false (44) |
| UserPreferencesDisableBookmarkEmail | boolean | 100% | DisableBookmarkEmail · false (44) |
| UserPreferencesDisableSharePostEmail | boolean | 100% | DisableSharePostEmail · false (44) |
| UserPreferencesActionLauncherEinsteinGptConsent | boolean | 100% | ActionLauncherEinsteinGptConsent · false (44) |
| UserPreferencesAssistiveActionsEnabledInActionLauncher | boolean | 100% | AssistiveActionsEnabledInActionLauncher · false (44) |
| UserPreferencesEnableAutoSubForFeeds | boolean | 100% | EnableAutoSubForFeeds · false (44) |
| UserPreferencesDisableFileShareNotificationsForApi | boolean | 100% | DisableFileShareNotificationsForApi · false (44) |
| UserPreferencesShowTitleToExternalUsers | boolean | 100% | ShowTitleToExternalUsers · true (38), false (6) |
| UserPreferencesShowManagerToExternalUsers | boolean | 100% | ShowManagerToExternalUsers · false (44) |
| UserPreferencesShowEmailToExternalUsers | boolean | 100% | ShowEmailToExternalUsers · false (44) |
| UserPreferencesShowWorkPhoneToExternalUsers | boolean | 100% | ShowWorkPhoneToExternalUsers · false (44) |
| UserPreferencesShowMobilePhoneToExternalUsers | boolean | 100% | ShowMobilePhoneToExternalUsers · false (44) |
| UserPreferencesShowFaxToExternalUsers | boolean | 100% | ShowFaxToExternalUsers · false (44) |
| UserPreferencesShowStreetAddressToExternalUsers | boolean | 100% | ShowStreetAddressToExternalUsers · false (44) |
| UserPreferencesShowCityToExternalUsers | boolean | 100% | ShowCityToExternalUsers · false (44) |
| UserPreferencesShowStateToExternalUsers | boolean | 100% | ShowStateToExternalUsers · false (44) |
| UserPreferencesShowPostalCodeToExternalUsers | boolean | 100% | ShowPostalCodeToExternalUsers · false (44) |
| UserPreferencesShowCountryToExternalUsers | boolean | 100% | ShowCountryToExternalUsers · false (44) |
| UserPreferencesShowProfilePicToGuestUsers | boolean | 100% | ShowProfilePicToGuestUsers · false (44) |
| UserPreferencesShowTitleToGuestUsers | boolean | 100% | ShowTitleToGuestUsers · false (44) |
| UserPreferencesShowCityToGuestUsers | boolean | 100% | ShowCityToGuestUsers · false (44) |
| UserPreferencesShowStateToGuestUsers | boolean | 100% | ShowStateToGuestUsers · false (44) |
| UserPreferencesShowPostalCodeToGuestUsers | boolean | 100% | ShowPostalCodeToGuestUsers · false (44) |
| UserPreferencesShowCountryToGuestUsers | boolean | 100% | ShowCountryToGuestUsers · false (44) |
| UserPreferencesShowForecastingChangeSignals | boolean | 100% | ShowForecastingChangeSignals · false (39), true (5) |
| UserPreferencesLiveAgentMiawSetupDeflection | boolean | 100% | LiveAgentMiawSetupDeflection · false (44) |
| UserPreferencesHideS1BrowserUI | boolean | 100% | HideS1BrowserUI · true (37), false (7) |
| UserPreferencesDisableEndorsementEmail | boolean | 100% | DisableEndorsementEmail · false (44) |
| UserPreferencesPathAssistantCollapsed | boolean | 100% | PathAssistantCollapsed · false (44) |
| UserPreferencesCacheDiagnostics | boolean | 100% | CacheDiagnostics · false (44) |
| UserPreferencesShowEmailToGuestUsers | boolean | 100% | ShowEmailToGuestUsers · false (44) |
| UserPreferencesShowManagerToGuestUsers | boolean | 100% | ShowManagerToGuestUsers · false (44) |
| UserPreferencesShowWorkPhoneToGuestUsers | boolean | 100% | ShowWorkPhoneToGuestUsers · false (44) |
| UserPreferencesShowMobilePhoneToGuestUsers | boolean | 100% | ShowMobilePhoneToGuestUsers · false (44) |
| UserPreferencesShowFaxToGuestUsers | boolean | 100% | ShowFaxToGuestUsers · false (44) |
| UserPreferencesShowStreetAddressToGuestUsers | boolean | 100% | ShowStreetAddressToGuestUsers · false (44) |
| UserPreferencesLightningExperiencePreferred | boolean | 100% | LightningExperiencePreferred · true (42), false (2) |
| UserPreferencesPreviewLightning | boolean | 100% | PreviewLightning · false (44) |
| UserPreferencesHideEndUserOnboardingAssistantModal | boolean | 100% | HideEndUserOnboardingAssistantModal · false (44) |
| UserPreferencesHideLightningMigrationModal | boolean | 100% | HideLightningMigrationModal · false (44) |
| UserPreferencesHideSfxWelcomeMat | boolean | 100% | HideSfxWelcomeMat · true (37), false (7) |
| UserPreferencesHideBiggerPhotoCallout | boolean | 100% | HideBiggerPhotoCallout · false (44) |
| UserPreferencesGlobalNavBarWTShown | boolean | 100% | GlobalNavBarWTShown · false (44) |
| UserPreferencesGlobalNavGridMenuWTShown | boolean | 100% | GlobalNavGridMenuWTShown · false (44) |
| UserPreferencesCreateLEXAppsWTShown | boolean | 100% | CreateLEXAppsWTShown · false (44) |
| UserPreferencesFavoritesWTShown | boolean | 100% | FavoritesWTShown · false (44) |
| UserPreferencesRecordHomeSectionCollapseWTShown | boolean | 100% | RecordHomeSectionCollapseWTShown · false (44) |
| UserPreferencesRecordHomeReservedWTShown | boolean | 100% | RecordHomeReservedWTShown · false (44) |
| UserPreferencesFavoritesShowTopFavorites | boolean | 100% | FavoritesShowTopFavorites · false (44) |
| UserPreferencesExcludeMailAppAttachments | boolean | 100% | ExcludeMailAppAttachments · false (44) |
| UserPreferencesSuppressTaskSFXReminders | boolean | 100% | SuppressTaskSFXReminders · false (44) |
| UserPreferencesSuppressEventSFXReminders | boolean | 100% | SuppressEventSFXReminders · false (44) |
| UserPreferencesPreviewCustomTheme | boolean | 100% | PreviewCustomTheme · false (44) |
| UserPreferencesHasCelebrationBadge | boolean | 100% | HasCelebrationBadge · false (44) |
| UserPreferencesUserDebugModePref | boolean | 100% | UserDebugModePref · false (44) |
| UserPreferencesSRHOverrideActivities | boolean | 100% | SRHOverrideActivities · false (44) |
| UserPreferencesNewLightningReportRunPageEnabled | boolean | 100% | NewLightningReportRunPageEnabled · false (44) |
| UserPreferencesReverseOpenActivitiesView | boolean | 100% | ReverseOpenActivitiesView · false (44) |
| UserPreferencesHasSentWarningEmail | boolean | 100% | HasSentWarningEmail · false (44) |
| UserPreferencesHasSentWarningEmail238 | boolean | 100% | HasSentWarningEmail238 · false (44) |
| UserPreferencesHasSentWarningEmail240 | boolean | 100% | HasSentWarningEmail240 · false (44) |
| UserPreferencesNativeEmailClient | boolean | 100% | NativeEmailClient · false (44) |
| UserPreferencesSendListEmailThroughExternalService | boolean | 100% | SendListEmailThroughExternalService · false (44) |
| UserPreferencesHideBrowseProductRedirectConfirmation | boolean | 100% | HideBrowseProductRedirectConfirmation · false (44) |
| UserPreferencesHideOnlineSalesAppTabVisibilityRequirementsModal | boolean | 100% | HideOnlineSalesAppTabVisibilityRequirementsModal · false (44) |
| UserPreferencesHideOnlineSalesAppWelcomeMat | boolean | 100% | HideOnlineSalesAppWelcomeMat · false (39), true (5) |
| UserPreferencesShowForecastingRoundedAmounts | boolean | 100% | ShowForecastingRoundedAmounts · false (39), true (5) |
| IsPortalEnabled | boolean | 100% | Is Portal Enabled · false (44) |
| IsExtIndicatorVisible | boolean | 100% | Show external indicator · false (44) |
| OutOfOfficeMessage | string | 100% | Out of office message |
| DigestFrequency | picklist | 100% | Chatter Email Highlights Frequency · D (39), N (5) |
| DefaultGroupNotificationFrequency | picklist | 100% | Default Notification Frequency when Joining Groups · N (44) |
| LastViewedDate | datetime | 2% | Last Viewed Date · 2026-09-29 04:22:48 … 2026-09-29 04:22:48 |
| LastReferencedDate | datetime | 2% | Last Referenced Date · 2026-09-29 04:22:48 … 2026-09-29 04:22:48 |
| IsProfilePhotoActive | boolean | 100% | Has Profile Photo · false (43), true (1) |

Never filled: Division, City, State, UserRoleId, DelegatedApproverId, ManagerId, SuAccessExpirationDate, OfflineTrialExpirationDate, OfflinePdaTrialExpirationDate, ContactId, AccountId, CallCenterId, PortalRole.
