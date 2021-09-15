# GmailZero
Windows GMail &amp; Google Cal client focused on day-to-day

Here at the inception this begins with the wishlist... can't believe i can't find an existing app that does a few calendar integration things i'm looking for, even commercial.

## Wishlist / Design Goals
1. create calendar event from email
1. support multiple reminders feature of google calendar
1. action button to forward existing calender event to another email (that's my poor man's approach to integrating with another calendar, i.e. work vs personal)
3. i've briefly considered whether to do a web app vs desktop app... i'm adept at React at this point so i know it would be doable in web but leaning towards a traditional desktop app to ensure the exact UX i'd want, including:
   1. ESC to minimize window (along with close = minimize option)... previously i would've wanted this to a be a min-to-systray, but with Windows 11, minimizing to taskbar seems like the more mainstream way to go
   1. taskbar badge for new email count (gotta have it)
4. i'd take a quick pulse of wherever msft currently looks to be headed for desktop apps but frankly i'm a WPF fanboi from wayback... especially since thank goodness they've doubled down on supporting it in .net core/5.0 and beyond! not at all impressed by the crazy amount of fragmentation msft has created in the desktop app space... UWP never got to feature parity with what WPF was already doing in 2010... xamarin was definitely cool for mobile and would've been nice if they'd gotten behind evolving that into WPF2.0, but that was officially deprecated in 2020 and now that lineage is rolled into MAUI for xplat... with WinUI out there for Windows only, but my impression is WinUI doesn't have feature parity with WPF yet either... this is all still baking in the oven but i guess we can code to WinUI directly or eventually? expect to target it from MAUI... obviously MAUI would be the starting point if you really want xplat but i don't... i always had fun running a hackintosh on the side (with apple silicon those days are over) and macOS has always been a sexy temptation but, especially now with fully integrated linux including X-Windows with WSL2, the availability of every little legacy app and tool there ever was, and FINALLY a real terminal, Windows is way to cozy to look anywhere else.
    - more thoughts - i'm not personally interested in xplat but to be an open project and cast the widest net for collaboration, it makes sense... looking around, the [Uno platform](https://platform.uno/) is probably the only real way to do this to include Linux right now... circa 2021-Q4 Msft is still saying MAUI for Linux must be driven by "the community".
    - what this means is the classic compromise of accepting lowest common denominator functionality, in this case that means WinUI will be the Windows target... hopefully an email client doesn't need to do anything all that fancy that runs into UX gaps on WinUI
6. i'd lean on the existing gmail web page for anything outside of my own day to day happy path to keep implementation as minimal as possible
7. common window layout with nav down left side, inbox list next, then current email pane and lastly vertical calendar panel on the right...
8. multiple inboxes! pretty killer feature i use in the gmail web app... basically it's the idea of showing more "folders" at once than just a primary inbox... couple this with gmail's amazingly robust (albeit unfriendly) filter rules and you can do powerful "auto cleansing", which is very [inbox zero](https://en.wikipedia.org/wiki/Merlin_Mann) zen... i like keeping a "pending" and "kids" view... pending is a manual move but kids vacuums up a ton of different inbound stuff via filters
9. common calendar views of either today only with slots for times -or- multiple dayswith just scheduled events showing
10. favorite folders up at the top of the left side nav
11. the obvious right mouse actions and buttons: delete, move to folder, reply, forward, move to calendar!, create new email (i tend to not want to blindly "archive", if i want to keep, i want to put in specific folder), mark as unread
12. common mark-as-read behavior as emails are opened
13. common keyboard nav, cursor up/down in inbox, tab through panels (again, ESC to minimize is a must!)
14. (seems like a nightmare feature) but it would be killer to have a robust "archive folder" ... i'm thinking a zip of emails printed to pdf along with bundling their attachements is probably the most "portable" approach... and maybe each email "thread/conversation" is a nested zip of leaf emails? i can't think of how you'd ever get something that could be reloaded as real emails... google has it's own extract-your-data facility, have to see what format those come out as
15. besides actual app features, any modern app needs a streamlined build process... i use msft DevOps at work but this would be a good opportunity to get up to speed on "github actions ci/cd"

## list of existing apps i've tried so far:
  - [Mailbird (commercial)](https://mailbird.com) - pretty nice in general but doesn't do wishlist #1 ([feature request #88155, created and ignored 2020-04](https://mailbird.featureupvote.com/suggestions/88155/calendar-convert-email-into-an-appointment-andor-task))
  - [emClient (free version)](https://www.emclient.com/) - actually does supports create event from email but not dragging to specific time slot, which is workable... but then it doesn't support wishlist #2, arrrg ([feature request #36464, created and ignored since 2013](https://forum.emclient.com/t/any-plans-to-support-multiple-reminders-for-calendar-events/36464))
  - [MailSpring](https://getmailspring.com/) - [calendar support forthcoming for many years](https://github.com/Foundry376/Mailspring/issues/199) => [latest issue tracking](https://community.getmailspring.com/t/calendar-support/85/13)
     - another spin on where to invest my energy would be seeing if i could grok the mailspring codebase enough to enhance it... it sounds like it's c++ at it's core ([one interesting article from the main dev](https://community.getmailspring.com/t/a-free-open-source-future-for-mailspring/484))... interesting, the UI is React inside of Electron... that's pretty cool! i happen to be pretty dang good at React at this point =)
     - [hmmm actually seems to be some work on calendar circa 2020-Q1](https://github.com/Foundry376/Mailspring/issues/1492)...
     - ok it's progress but more than a year later it's still read-only with a message: "Calendar is launching later this year"... gotta hand it to main dev @BenGotow ... cautionary story of how big of a lift this is to do solo =)
     - at least he's got somewhat of a commercial model cooking for the pro features... hopefully that will keep this project alive for the long haul... nothing worse than an abandoned email client
     - and this UI looks really nice... the intro setup flow is beautiful work, GSuite called out properly, a truly pleasurable experience... especially after just stumbling through evolution's startup config =)
  - there's of course tons of email only clients out there, i.e. calendar support isn't on the radar at all
  - [Zimbra (Desktop)](https://www.zimbra.com/downloads/zimbra-desktop/) - DANG! discontinued in 2019, and now web client only... this looks like it was killer

## best email clients posts
- https://medium.com/issuehunt/10-open-source-mail-clients-fd7886bff999

## actual contenders!
- [Evolution](https://riseup.net/en/email/clients/evolution) - Linux only but now that Windows runs WSLg that's not a deal breaker... it does the basic create event from email! no drag drop unfortunately... but the setup and initial layout are very usable... will give this a go!

## development references
- https://developers.google.com/calendar/api/quickstart/dotnet
- https://github.com/jstedfast/MailKit
- https://jasonwatmore.com/post/2020/07/15/aspnet-core-3-send-emails-via-smtp-with-mailkit
- https://docs.github.com/en/actions/guides/building-and-testing-net
