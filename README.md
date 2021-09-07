# GmailZero
Windows GMail &amp; Google Cal client focused on day-to-day

Here at the inception this begins with the wishlist... can't believe i can't find an existing app that does a few calendar integration things i'm looking for, even commercial.

## Wishlist / Design Goals
1. create calendar event from email
1. support multiple reminders feature of google calendar
1. i've briefly considered whether to do a web app vs desktop app... i'm adept at React at this point so i know it would be doable in web but leaning towards a traditional desktop app to ensure the exact UX i'd want, including:
   1. ESC to minimize window (along with close = minimize option)... previously i would've wanted this to a be a min-to-systray, but with Windows 11, minimizing to taskbar seems like the more mainstream way to go
   1. taskbar badge for new email count (gotta have it)
 1. i'd take a quick pulse of wherever msft currently looks to be headed for desktop apps but frankly i'm a WPF fanboi from wayback... especially since thank goodness they've doubled down on supporting it in .net core/5.0 and beyond! not at all impressed by the crazy amount of fragmentation msft has created in the desktop app space... UWP never got to feature parity with what WPF was already doing in 2010... xamarin was definitely cool for mobile and would've been nice if they'd gotten behind evolving that into WPF2.0, but that was officially deprecated in 2020 and now that lineage is rolled into MAUI for xplat... with WinUI out there for Windows only, but my impression is WinUI doesn't have feature parity with WPF yet either... this is all still baking in the oven but i guess we can code to WinUI directly or eventually? expect to target it from MAUI... obviously MAUI would be the starting point if you really want xplat but i don't... i always had fun running a hackintosh on the side (with apple silicon those days are over) and macOS has always been a sexy temptation but, especially now with fully integrated linux including X-Windows with WSL2, the availability of every little legacy app and tool there ever was, and FINALLY a real terminal, Windows is way to cozy to look anywhere else.
 1. i'd lean on the existing gmail web page for anything outside of my own day to day happy path to keep implementation as minimal as possible
 1. common window layout with nav down left side, inbox list next, then current email pane and lastly vertical calendar panel on the right...
 1. multiple inboxes! pretty killer feature i use in the gmail web app... basically it's the idea of showing more "folders" at once than just a primary inbox... couple this with gmail's amazingly robust (albeit unfriendly) filter rules and you can do powerful "auto cleansing", which is very [inbox zero](https://en.wikipedia.org/wiki/Merlin_Mann) zen... i like keeping a "pending" and "kids" view... pending is a manual move but kids vacuums up a ton of different inbound stuff via filters
 1. common calendar views of either today only with slots for times -or- multiple dayswith just scheduled events showing
 1. favorite folders up at the top of the left side nav
 1. the obvious right mouse actions and buttons: delete, move to folder, reply, forward, move to calendar!, create new email (i tend to not want to blindly "archive", if i want to keep, i want to put in specific folder), mark as unread
 1. common mark-as-read behavior as emails are opened
 1. common keyboard nav, cursor up/down in inbox, tab through panels (again, ESC to minimize is a must!)

## list of existing apps i've tried so far:
  - [Mailbird (commercial)](https://mailbird.com) - pretty nice in general but doesn't do wishlist #1 ([feature request #88155, created and ignored 2020-04](https://mailbird.featureupvote.com/suggestions/88155/calendar-convert-email-into-an-appointment-andor-task))
  - [emClient (free version)](https://www.emclient.com/) - actually does supports create event from email but not dragging to specific time slot, which is workable... but then it doesn't support wishlist #2, arrrg ([feature request #36464, created and ignored since 2013](https://forum.emclient.com/t/any-plans-to-support-multiple-reminders-for-calendar-events/36464))
  - there's of course tons of email only clients out there, i.e. calendar support isn't on the radar at all
