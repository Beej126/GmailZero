# GmailZero
Windows GMail &amp; Google Cal client focused on day-to-day

Here at the inception this begins with the wishlist... can't believe i can't find an existing app that does a few calendar integration things i'm looking for, even commercial.

## Wishlist / Design Goals
1. **Full calendar integration**
   1. #1 **create calendar event from email** (missing from mailbird)
   1. support **multiple reminders** feature of google calendar (missing from emClient)
   1. **forward event** to another address - poor man's approach to integrating with another calendar, i.e. work vs personal
   1. common "today at a glance" views - with either today only showing slots for all hours -or- multiple days with just scheduled events showing
1. **Gmail adjunct strategy** - lean on the existing gmail web page for anything outside of my own day to day happy path to keep implementation as minimal as possible
1. common window layout with nav down left side, inbox list next, then current email pane and lastly vertical calendar panel on the right...
1. multiple inboxes! pretty killer feature i use in the gmail web app... basically it's the idea of showing more "folders" at once than just a primary inbox... couple this with gmail's amazingly robust (albeit unfriendly) filter rules and you can do powerful "auto cleansing", which is very [inbox zero](https://en.wikipedia.org/wiki/Merlin_Mann) zen... i like keeping a "pending" and "kids" view... pending is a manual move but kids vacuums up a ton of different inbound stuff via filters
1. **favorite folders** - up at the top of the left side nav (missing from mailbird)
1. **move-to-folder** action button (with favorite folders at the top of list) (missing from mailbird)
1. the obvious right mouse actions and buttons: delete, move to folder, reply, forward, move to calendar!, create new email (i tend to not want to blindly "archive", if i want to keep, i want to put in specific folder), mark as unread
1. common mark-as-read behavior as emails are opened
1. common keyboard nav, cursor up/down in inbox, tab through panels (again, ESC to minimize is a must!)
1. **export folder** - seems like a nightmare feature to implement correctly
   1. Evolution (listed below) is a good longstanding source of proper execution on several features including export - they dump to MBOX format which i now see is a well established standard that can be opened and read AND SEARCHED by many 3rd party tools... that's the way to go for this
   1. <s>initially thinking a zip of emails printed to pdf along with bundling their attachements is probably the most "portable" approach... and maybe each email "thread/conversation" is a nested zip of leaf emails? i can't think of how you'd ever get something that could be reloaded as real emails</s>
   1. google has it's own extract-your-data facility, have to see what format those come out as

## app architecture
1. besides actual app features, any modern app needs a streamlined build process... i use msft DevOps at work but this would be a good opportunity to get up to speed on github actions
1. whether to do a web app vs desktop app... i'm deep into a very dense UX internal LoB React app during the day so i know i could do this in web only but still miss the sweet intersection of real C# object collections with built in onchange/isdirty along with M-V-VM style databinding like WPF
1. there's also a handful of desktop window features that i believe are only possible via some kind of true desktop app wrapper (electron, react native, etc)
  1. ESC to minimize window (along with close = minimize option)... previously i would've wanted this to a be a minimize to _systray_, but with Windows 11, minimizing to taskbar seems like the new way to go
  1. taskbar badge for new email count (gotta have it)
1. state of the Windows Desktop DIS-union
  1. right up front i'm a WPF fanboi from wayback... very cool msft has doubled down on supporting .net core
  1. i guess UWP is now rolled into WinUI... has either reached feature parity with WPF yet?
  1. i did a fair amount of xamarin on mobile ... that lineage is now rolled into MAUI, which is additionally targeting desktop apps, yet everybody's cranky that team doesn't have the bandwidth to include linux
  1. looking around, the [Uno platform](https://platform.uno/) is probably the only real way to do this to include Linux right now circa 2021-Q4
     - apparenlty they leverage WinUI for their Windows target
     - this smells like it would be the classic compromise of accepting lowest common denominator functionality
  1. to be fair, an email client probably? doesn't need to do anything all that fancy and lowest denom might not be a real limitiation
  1. yet chasing the xplat holy grail really seems to leave all these rolling efforts perpetually short of tried and true feature parity with WPF... for this kind of personal project, i'm not really inclined to worry about xplat... macOS and Linux are definitely cool but the only real reason for me to spend precious energy on xplat would be to appeal for outside help and i'm not inclined for that on this project ... this is going to be highly tailored to my workflows, not trying to please anybody else.
  1. Windows is way too cozy to envy anywhere else anymore - fully integrated linux including X-Windows GUI apps on WSL2/WSLg, and the longstanding availability of every little legacy app and tool there ever was, and FINALLY a real terminal

## list of existing apps i've tried so far:
  - [Mailbird (commercial)](https://mailbird.com) - pretty nice in general but doesn't do wishlist #1 ([feature request #88155, created and ignored 2020-04](https://mailbird.featureupvote.com/suggestions/88155/calendar-convert-email-into-an-appointment-andor-task))
  - [emClient (free version)](https://www.emclient.com/) - actually does supports create event from email but not dragging to specific time slot, which is workable... but then it doesn't support wishlist #2, arrrg ([feature request #36464, created and ignored since 2013](https://forum.emclient.com/t/any-plans-to-support-multiple-reminders-for-calendar-events/36464))
  - [MailSpring](https://getmailspring.com/) - [calendar support forthcoming for many years](https://github.com/Foundry376/Mailspring/issues/199) => [latest issue tracking](https://community.getmailspring.com/t/calendar-support/85/13)
     - another spin on where to invest my energy would be seeing if i could grok the mailspring codebase enough to enhance it... it sounds like it's c++ at it's core ([one interesting article from the main dev](https://community.getmailspring.com/t/a-free-open-source-future-for-mailspring/484))... interesting, the UI is React inside of Electron... that's pretty cool! i happen to be pretty dang good at React at this point =)
     - [hmmm actually seems to be some work on calendar circa 2020-Q1](https://github.com/Foundry376/Mailspring/issues/1492)...
     - ok it's progress but more than a year later none of my events are showing and there's a message: "Calendar is launching later this year"... gotta hand it to main dev @BenGotow ... cautionary story of how big of a lift this is to do solo =)
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
