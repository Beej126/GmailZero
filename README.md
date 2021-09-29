# GmailZero
This idea started out as a simple GMail/GCal Windows app focused on day-to-day

The calendar aspects quickly take front stage... for me (especially after reading this [great Wired article](https://www.wired.com/story/to-do-apps-failed-productivity-tools/)) so much of what comes through the inbox MUST wind up on your calendar... the article coins the strategy as "time blocking"... 

and the crystal clear nutshell is this: <mark><span style="background-color: yellow">don't focus on to-do lists anymore, put everything you want to accomplish on your calendar</span></mark>, and anything new that comes long must either fit into the gaps or replace something... this quite literally shows you exactly what you do and don't have time to accomplish... keeping lists beyond that is not only pointless, it saps precious psychological energy.

## Really thinking this through
- to really do this right, there's no getting around the need to integrate one's work calendar with their personal calendar...
- they really have to be one and the same, the sum total of everything that you're booked for... especially these days now that we're working a lot more from home and weaving life and work together in more dynamic ways than what used to be a more cut and dried 9-5
- for me that means Office 365 / Outlook for work and GMail/GCall for personal...
- after all these years, Outlook still has at least two critical gaps for my needs:
  1. can't do multiple recurring reminders!?
  2. you can visually overlay two calendars rather nicely (including your external google cal!) in the main calendar view but they don't support doing that in the "To Do" panel off to the right of your inbox, arrrg!!!
- another immovable constraint is the published work calendar is the primary means for others to see free time and book meetings... at least we have this well established at work, too bad that's not so standardized with everyone we interact with in our personal lives... we tend to all have our own calendars and they're not shared with eachother... there are apps that sit here and bridge that gap in clever ways (e.g. [Calendly](https://calendly.com)).
- so far the only way i can see this all coming together is an app sitting in the middle, doing all the brute force to put everything on both calendars
  - as mentioned above, everything needs to be on outlook,
  - but with outlook's reminder gap, we also have to put it all on google cal just to be reminded properly, that is wild
  - and it's not like it all happens in this magic app alone, by getting events on the google cal, that leverages getting reminders on our mobile devices, which is a huge part of the equation
- there are of course tons of sync tools, [started list below](#sync-tools)
- it seems like you could consider gmail the master and sync everything back to outlook...
- but there are bound to be glitches there... one critical behavior to check is how recurring appointments copy over

## Wishlist / Design Goals
1. this essentially starts with mailbird as a decent reference point UI wise and wanting to fix some crucial annoyances
2. **Full calendar integration**
   1. #1 **create calendar event from email** (missing from mailbird)
   2. support **multiple reminders** feature of google calendar (missing from emClient)
   3. **forward event** to another address - poor man's approach to integrating with another calendar, i.e. work vs personal
   4. common "today at a glance" views - with either today only showing slots for all hours -or- multiple days with just scheduled events showing
3. common window layout with folder nav down left side, inbox list in the middle, current email reading pane next to the right
4. and very important, **a vertical UNIFIED calendar panel on the far right**...
5. with drag and drop from the unified inbox to a time slot on the calendar
6. action buttons - typical button bar above the inbox vs the reading pane so they're always visible even for small window (mailbird annoyance)
7. multiple inboxes! pretty killer feature i use in the gmail web app... basically it's the idea of showing more "folders" at once than just a primary inbox... couple this with gmail's amazingly robust (albeit unfriendly) filter rules and you can do powerful "auto cleansing", which is very [inbox zero](https://en.wikipedia.org/wiki/Merlin_Mann) zen... i like keeping a "pending" and "kids" view... pending is a manual move but kids vacuums up a ton of different inbound stuff via filters
8. **favorite folders** - up at the top of the left side nav (missing from mailbird)
9. **move-to-folder** action button (with favorite folders at the top of list)
10. the obvious right mouse actions and buttons: delete, move to folder, reply, forward, move to calendar!, create new email (i tend to not want to blindly "archive", if i want to keep, i want to put in specific folder), mark as unread
11. common mark-as-read behavior as emails are opened
12. common keyboard nav, cursor up/down in inbox, tab through panels (again, ESC to minimize is a must!)

## Gmail "adjunct" strategy
- lean on the existing gmail web page for anything outside of my own day to day happy path to keep implementation as minimal as possible
- and probably just run gmail in an embedded web control to have it close it at hand
1. print email - why try to reinvent all that when gmail web such does a great job 
1. export folder
    1. Evolution (listed below) is a good longstanding source of proper execution on several features including export - they dump to MBOX format which i now see is a well established standard that can be opened and read AND SEARCHED by many 3rd party tools... that's the way to go for this
    1. google has it's own extract-your-data facility, have to see what format those come out as

## app architecture
1. besides actual app features, any modern app needs a streamlined build process... i use msft DevOps at work but this would be a good opportunity to get up to speed on github actions
2. whether to do a web app vs desktop app... i'm deep into a very dense UX internal LoB React app during the day so i know i could do this in web only but still miss the sweet intersection of real C# object collections with built in onchange/isdirty along with M-V-VM style databinding like WPF
3. there's a handful of crucial desktop window features that i believe are only possible via some kind of true desktop app wrapper (electron, react native, etc)
   1. ESC to minimize window (along with close = minimize option)... previously i would've wanted this to a be a minimize to _systray_, but with Windows 11, minimizing to taskbar seems like the new way to go
   2. taskbar badge for new email count (gotta have it)
4. to xplat or not, -OR- the state of the Windows Desktop DIS-union
   1. right up front i'm a WPF fanboi from wayback... very cool msft has doubled down on supporting .net core
   2. i guess UWP is now rolled into WinUI... has either reached feature parity with WPF yet?
   3. i did a fair amount of xamarin on mobile ... that lineage is now rolled into MAUI, which is additionally targeting desktop apps, yet everybody's cranky that team doesn't have the bandwidth to include linux
   4. looking around, the [Uno platform](https://platform.uno/) is probably the only real way to do this to include Linux right now circa 2021-Q4
      - apparenlty they leverage WinUI for their Windows target
      - this smells like it would be the classic compromise of accepting lowest common denominator functionality
   5. to be fair, an email client probably? doesn't need to do anything all that fancy and lowest denom UI might not be a real limitiation
   6. yet chasing the xplat holy grail really seems to leave all these rolling efforts perpetually short of tried and true feature parity with WPF... for this kind of personal project, i'm not really inclined to worry about xplat... macOS and Linux are definitely cool but the only real reason for me to spend precious energy on xplat would be to appeal for outside help and i'm not inclined for that on this project ... this is going to be highly tailored to my workflows, not trying to please anybody else.
   7. despite the chaotic spillover from xplat into Windows desktop app dev, the Windows platform is still way too cozy to envy anywhere else anymore - adding fully integrated linux including X-Windows GUI apps via WSL2/WSLg on top of the longstanding availability of every little legacy Windows app and tool there ever was, along with FINALLY a robust Terminal, is a killer combo
   8. ha brilliant, good ol' [Delphi](https://www.embarcadero.com/products/delphi) is still kicking and apparently targets Windows, Mac, Linux AND iOS, Andoid!? those bloody rascals! ... funny thing, i am a huuge Borland and Delphi fanboi going back even further than WPF... nobody will remember this but i still remember the vestiges of how circa 2003 / Dephi 5 they shifted something low level completely over to the TClientDataSet, and broke the longstanding "cached updates" functionality that we were all in on with our LoB app... to Borland's credit, they were going after the future ... in this case it was the innevitible shift from client-server to 3-tiered... looking back at old posts, they were already making this move in Delphi 3 circa 1999!!! at the time we were of course very pissed to be innocent bystanders in that tidal wave of change, with nobody able to give us the time of day... forcing everything into a new paradigm without feature parity felt like the kind betrayal to expect from msft vs Borland... it felt like an artificial corporate decision vs engineering to break the old working bits due to the new bits... in hindsight, we were probably doing more advanced relational database implementation with Dephi than most shops achieve even to this day, and for better or worse, that meant nobody else cared enough to complain along side us.

## list of existing apps i've tried so far:
  - [Mailbird (commercial)](https://mailbird.com) - pretty nice in general but doesn't do wishlist #1 ([feature request #88155, created and ignored 2020-04](https://mailbird.featureupvote.com/suggestions/88155/calendar-convert-email-into-an-appointment-andor-task))
  - [emClient (free version)](https://www.emclient.com/) - actually does supports create event from email but not dragging to specific time slot, which is workable... but then it doesn't support wishlist #2, arrrg ([feature request #36464, created and ignored since 2013](https://forum.emclient.com/t/any-plans-to-support-multiple-reminders-for-calendar-events/36464))
  - [MailSpring](https://getmailspring.com/) - [calendar support forthcoming for many years](https://github.com/Foundry376/Mailspring/issues/199) => [latest issue tracking](https://community.getmailspring.com/t/calendar-support/85/13)
     - another spin on where to invest my energy would be seeing if i could grok the mailspring codebase enough to enhance it... it sounds like it's c++ at it's core ([one interesting article from the main dev](https://community.getmailspring.com/t/a-free-open-source-future-for-mailspring/484))... interesting, the UI is React inside of Electron... that's pretty cool! i happen to be pretty dang good at React at this point =)
     - [hmmm actually seems to be some work on calendar circa 2020-Q1](https://github.com/Foundry376/Mailspring/issues/1492)...
     - ok it's progress but more than a year later none of my events are showing and there's a message: "Calendar is launching later this year"... gotta hand it to main dev @BenGotow ... cautionary story of how big of a lift this is to do solo =)
     - at least he's got somewhat of a commercial model cooking for the pro features... hopefully that will keep this project alive for the long haul... nothing worse than an abandoned email client project (as i look in the mirror ;)
     - and this UI looks really nice... the intro setup flow is beautiful work, GSuite called out properly, a truly pleasurable experience... especially after just stumbling through evolution's startup config =)
  - there's of course tons of email only clients out there, i.e. calendar support isn't on the radar at all
  - [Zimbra (Desktop)](https://www.zimbra.com/downloads/zimbra-desktop/) - DANG! discontinued in 2019, and now web client only... this looks like it was killer

## best email clients posts
- https://medium.com/issuehunt/10-open-source-mail-clients-fd7886bff999

## actual contenders!
- [Evolution](https://riseup.net/en/email/clients/evolution) - Linux only but now that Windows runs WSLg that's not a deal breaker... it does the basic create event from email! no drag drop unfortunately... but the setup and initial layout are very usable... will give this a go!

## sync tools
- https://www.makeuseof.com/tag/how-to-sync-microsoft-outlook-with-google-calendar/

## development references
- https://developers.google.com/calendar/api/quickstart/dotnet
- https://github.com/jstedfast/MailKit
- https://jasonwatmore.com/post/2020/07/15/aspnet-core-3-send-emails-via-smtp-with-mailkit
- https://docs.github.com/en/actions/guides/building-and-testing-net
- https://docs.microsoft.com/en-us/microsoft-edge/webview2/get-started/wpf
- https://weblog.west-wind.com/posts/2021/Jan/14/Taking-the-new-Chromium-WebView2-Control-for-a-Spin-in-NET-Part-1
- Infragistics has a [WPF sample demo that mocks a basic Outlook'ish UI](https://www.infragistics.com/resources/sample-applications/infragistics-wpf-igoutlook)... it's all hard wired to fake data but it might be a nice starting point
  - i've successfully upgraded it to .Net 5.0 (thank you [Upgrade Assistant Tool](https://dotnet.microsoft.com/platform/upgrade-assistant)!!!) along with the tweaks required  to align with infragistics latest packages ([v21.1](https://www.infragistics.com/support/product-lifecycle))
