# Salah Tracker — Product & Implementation Specification

## 1. Project Goal
Build a simple, modern **Salah Tracker** for tracking the five daily prayers in Lahore, Pakistan. The interface must be calm, minimal, easy to understand, and written entirely in English. Avoid clutter, long paragraphs, excessive cards, and unnecessary colors.

## 2. Platform — Website Only
- Build a responsive website / web app that works in desktop and mobile browsers.
- Do not build a native Android app, APK, or mobile-app package.
- Use a sidebar on desktop and a compact responsive navigation pattern on small screens.
- Prioritize the website experience only; Android packaging is out of scope unless requested separately.

## 3. Visual Design
- **Main background:** warm beige.
- **Primary buttons and key actions:** dark forest green.
- **Supporting colors:** cream, white, and restrained muted gold only when useful.
- **Style:** modern, minimal, spacious, readable, subtle rounded corners, simple line icons.
- Give each of the five prayers its own distinct, consistent icon.
- Use dark green for active/selected states. Do not make the UI highly colorful.
- Use clear typography and short labels. Avoid large blocks of explanatory text on the dashboard.
- Provide a light/dark mode only if it can be implemented without making the first version complicated; the default theme is beige and dark green.

## 4. Main Dashboard
Show the five daily prayers in a vertical list/column. Each prayer row should display:
- Its individual icon and name: Fajr, Dhuhr, Asr, Maghrib, or Isha.
- Today's prayer start time.
- The end of its prayer window (when it becomes Qaza), where applicable.
- A simple status control with exactly three options: **Yes / Ada**, **No / Missed**, and **Qaza / prayed late**.
- A clear visual indication of the selected status.

The next upcoming prayer must be visually emphasized with a **bold prayer name** and a subtle dark-green highlight. Determine the next prayer using Lahore local time and today's calculated prayer schedule. Handle the transition after Isha and into the next day's Fajr correctly.

Keep the dashboard focused on today's prayers, the next prayer, a short motivational message, and the daily goal. Do not add a detailed history/calendar in this minimal first version.

## 5. Prayer Details
When the user selects a prayer row or its icon, open a compact detail view showing:
- Prayer name and icon.
- Today's start time and the time its prayer window ends / becomes Qaza.
- A short explanation of the prayer's importance.
- One brief, authentic Quran or Hadith reference related to prayer, with source attribution.

Keep the detail view concise. Do not invent Quran quotations, Hadith wording, references, or religious rulings. If a verified reference cannot be provided, omit it rather than fabricate one. Explain timing rules carefully and avoid presenting disputed fiqh details as universal.

## 6. Lahore Prayer Timings
- The app is configured for **Lahore, Punjab, Pakistan only** in this version. Do not show a city selector.
- Calculate prayer times automatically for the current date using Lahore coordinates and the Asia/Karachi time zone.
- Use a reliable prayer-time calculation library rather than hard-coded times. Prayer times must update with the date and daylight/seasonal changes.
- Default calculation settings for Pakistan: **University of Islamic Sciences, Karachi** calculation method and **Hanafi Asr**. Keep these settings in one clearly named configuration location so they can be changed later if needed.
- Show the calculated schedule's source/method in a small settings/about area if practical.
- Prayer window end times must be based on the calculated schedule and clearly defined rules: Fajr ends at sunrise; Dhuhr ends when Asr begins; Asr ends at sunset; Maghrib ends when Isha begins; Isha's end rule must follow the chosen calculation/fiqh convention and be documented. Do not label a time as “Qaza” unless the rule used to determine it is clear.
- Handle calculation errors gracefully; never silently display fake or hard-coded prayer times as if they were live calculations.

## 7. Prayer Status Rules
Each prayer for each date can have one of these statuses:
- **Ada (Yes):** the user marks the prayer as performed within its time.
- **Missed (No):** the user marks that the prayer was not performed.
- **Qaza:** the user marks that the prayer was performed after its prayer window ended.

Allow the user to change a status if they tapped the wrong option. Persist the chosen status for the correct prayer and date. Do not automatically mark a prayer as missed or Qaza solely because time passed; let the user choose the status.

## 8. Manual Qaza Counter
- Include a separate manual Qaza counter for each prayer: Fajr, Dhuhr, Asr, Maghrib, and Isha.
- Each prayer has its own count, with simple **+** and **−** controls.
- Never automatically increase the manual counter when the user selects “Qaza” for today's prayer. The daily status and the outstanding Qaza count are separate records.
- Prevent accidental negative counts and save changes immediately.
- Use concise labels, such as “Fajr Qaza: 12”.

## 9. Motivation and Daily Goal
- Include a simple daily goal of completing all five prayers (5/5).
- Show progress in a compact format, such as “3 of 5 completed”. Count only prayers marked Ada toward the on-time goal; display Qaza separately and do not count it as on-time Ada.
- Show one short, gentle motivational line. Also show a brief completion message when all five prayers are marked Ada.
- Keep messages respectful, encouraging, and non-judgmental. Avoid guilt-based language and do not overwhelm the dashboard with text.

## 10. Notifications
- **No prayer notifications in this version.** Do not implement notification permissions, reminders, or notification settings.

## 11. Data Storage and Privacy
- Save prayer statuses, manual Qaza counts, and preferences locally so they remain available after the app is closed or refreshed.
- The first version must work without requiring an account or login.
- Keep data local to the device/browser. Do not add a backend, analytics, or cloud sync unless requested later.
- Make date-specific records so a status for one day does not overwrite another day's status, even though a full history screen is not included in this version.

## 12. Minimal Navigation
Keep navigation limited to the essentials:
1. **Today** — five prayer rows, timings, next prayer, daily progress, and motivation.
2. **Qaza Counter** — separate manual counts for the five prayers.
3. **Settings / About** — theme preference if implemented, Lahore calculation method information, and app information.

The selected prayer's details may open from the Today screen as a compact panel or modal; it does not need a separate permanent navigation item.

## 13. Accessibility and Usability
- Make all status choices understandable without relying on color alone; include visible text labels.
- Ensure buttons and text are readable on beige and dark-green surfaces.
- Support keyboard navigation and visible focus states on the web.
- Use responsive spacing so the prayer list remains usable on a narrow phone screen.
- Include loading, empty, and calculation-error states.

## 14. Implementation Roadmap
1. Set up the responsive website shell and beige/dark-green design system.
2. Build the five-prayer dashboard with individual icons and status controls.
3. Integrate automatic Lahore prayer-time calculations with the Karachi method and Hanafi Asr setting.
4. Determine and bold the next upcoming prayer; calculate each prayer's window-end time according to the documented rules.
5. Add the selected-prayer detail panel with concise importance text and verified Quran/Hadith references.
6. Add the independent manual Qaza counters.
7. Add the daily 5/5 goal and short motivational messages.
8. Persist data locally and test reloads, date changes, midnight transitions, and responsive layouts.
9. Verify that no notifications, login, cloud backend, or unnecessary history screen have been added.

## 15. Acceptance Checklist
- [ ] App name is “Salah Tracker” and all interface text is in English.
- [ ] Beige is the main background; dark green is used for primary buttons and selected states.
- [ ] Five prayers appear in a clean vertical list, each with its own icon.
- [ ] Each prayer shows its calculated start time and prayer-window end time.
- [ ] Status choices are Ada, Missed, and Qaza; the user can correct a selection.
- [ ] The next upcoming prayer is bold and updates with local time.
- [ ] Selecting a prayer shows its timings, concise importance, and verified religious reference.
- [ ] Lahore timings update automatically by date and use the configured calculation method.
- [ ] Each prayer has an independent manual Qaza count with +/− controls.
- [ ] Daily progress and gentle motivation are visible without clutter.
- [ ] No prayer notifications or login are required.
- [ ] Data persists locally after closing or refreshing the app.
- [ ] The website layout works on desktop and mobile browser sizes.
- [ ] No native Android app or APK is built as part of this project.
