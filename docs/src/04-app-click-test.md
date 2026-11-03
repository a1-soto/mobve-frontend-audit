# App click test: every control and where it leads

Date: 2026-11-03. Staging app, role Owner. Every button, tab, menu item, disclosure and link on each screen was inspected. Controls that only filter, navigate, open or close were clicked; links were requested to check their destination. Controls that write, send, download or end the session were listed and not clicked. Filters were restored afterwards. No script errors were raised.

## 1. Results by screen

| Screen | Result |
|---|---|
| Shell | Sidebar links go to their routes; property selector filters scope and buildings and was restored; building selector, Emma AI dialog and user menu open and close with Escape; mobile drawer works |
| Dashboard | Refresh, Delta, Reset filters, 8 info panels and Total or Average work; KPI cards and day bars link to filtered Maintenance (200); View all goes to Call Log |
| Maintenance | Summary cards, 8 stage filters, Reset, List, Board and Group by category work; pagination disabled with 7 results; View request opens the detail, Back returns |
| Appointments | Add appointment dialog opens and closes; Overview and Pipeline switch; week, day and month navigation moves the range; Review prospect and prospect cards open |
| Call Log | Refresh and Reset filters show no change (empty list, default filters) |
| Settings | 19 pages open; 5 Fix links and Open inventory workspace answer 200; Preview impact works; Properties: first row expanded, other rows and Manage showed no measurable change |

## 2. Problems found

1. Resident requests cannot load and Try again does nothing.
2. Save buttons are enabled with nothing changed on nine pages (Company profile, Profile, Maintenance, Hours and coverage, Inventory, Leasing and appointments, Notifications, Privacy and retention, Voice assistant), while Save role, Save call answering and phone routing stay disabled until a change.
3. Refresh data on Maintenance, Appointments and Call Log gives no visible confirmation.
4. Dashboard day bars link to Maintenance even when the value is 0.
5. Dashboard links with query parameters reload the whole page.
6. The Inventory screen is reachable only from a Settings link.
7. "How these metrics work" shows no effect.
8. The Call Log did not request new data after changing the property (check with populated data).

## 3. Not clicked on purpose

Log out and Sign out; Export CSV and Download acceptance receipt; every Save; Send code and Send test page (5); Upload document; Remove, Invite member, Create department, Create draft policy, Run draft checks, Log verified-intake request, Add closure, Add target, Add 14-day coverage, Add to calendar; about 30 switches, checkboxes and radio buttons.

Test these with a disposable account or approved test data, and confirm what each one triggers (messages, calls, billing, audit entries).
