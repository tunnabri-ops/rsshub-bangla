# RSSHub Bangla routes — কোন route দিয়ে কী পাবেন

> **সব route যাচাই করা হয়েছে RSSHub-এর সোর্স থেকে (2026-11-25):**
> প্রতিটি route-এর `path:` নেওয়া হয়েছে
> `github.com/DIYgod/RSSHub` repo-র `lib/routes/<নাম>/` ফাইল থেকে।
> docs.rsshub.app curl-কে 403 দেয়, তাই route যাচাই করা হয়েছে সোর্স কোড থেকে —
> এটাই সবচেয়ে নির্ভরযোগ্য জায়গা।

## ⚠️ বাংলা নিয়ে সত্যি কথাটা আগে

**RSSHub-এ বাংলা / Bengali / Bangladesh-এর কোনো route নেই।**
`lib/routes/`-এর ২,৯৯৪টি route ডিরেক্টরি খুঁজে দেখা হয়েছে — "bang" দিয়ে
শুধু এগুলো মেলে: `bangumi.moe`, `bangumi.online`, `bangumi.tv` (জাপানি অ্যানিমে
সাইট, বাংলার সঙ্গে সম্পর্ক নেই) আর `geekbang` (চীনা টেক সাইট)।

বাংলা খবরের জন্য RSSHub route খুঁজবেন না — সরাসরি RSS ফিড ব্যবহার করুন।
যাচাই করা ৫টি বাংলা ফিডের OPML আছে `newsblur-bangla/bangla-feeds.opml`-এ
(Prothom Alo, BBC Bengali, bdnews24 Bangla, Daily Star, Channel i Online)।

আরও একটা: **Reddit-এর route-ও আর নেই** — `lib/routes/reddit` এখন 404।
পুরনো গাইডে `/reddit/...` দেখলে সেটা আর চলবে না।

## যাচাই করা route-গুলো

নিচের প্রতিটি route-এর pattern সোর্স থেকে নেওয়া। উদাহরণ কলামের `:xxx`
জায়গায় বসানো মানগুলো (যেমন চ্যানেল ID, topic-এর নাম) সোর্স সাইটের আসল
মান দিয়ে বদলে নিতে হবে — pattern-টাই যাচাই করা অংশ।

| Route | কী পাবেন | উদাহরণ |
|---|---|---|
| `/bbc/:site?/:channel?` | BBC খবর | `http://localhost:1200/bbc` |
| `/bbc/topics/:topic` | BBC-র কোনো বিষয় (topic) | `http://localhost:1200/bbc/topics/climate` |
| `/github/repos/:user/:type?/:sort?` | কোনো GitHub ইউজারের repo | `http://localhost:1200/github/repos/torvalds` |
| `/github/trending/:since/:language/:spoken_language?` | GitHub trending repo | `http://localhost:1200/github/trending/daily` |
| `/youtube/channel/:id/:routeParams?` | YouTube চ্যানেলের ভিডিও | `http://localhost:1200/youtube/channel/UC_x5XG1OV2P6uZZ5FSM9Ttw` |
| `/youtube/playlist/:id` | YouTube প্লেলিস্ট — `:id`-এর জায়গায় আপনার প্লেলিস্ট URL-এর `list=`-এর পরের অংশ বসান | `http://localhost:1200/youtube/playlist/` + আপনার প্লেলিস্টের ID |
| `/hackernews/:section?/:type?/:value?/:minComments?` | Hacker News | `http://localhost:1200/hackernews` |
| `/apnews/rss/:category?` | AP News | `http://localhost:1200/apnews/rss` |
| `/aljazeera/:language?/rss` | Al Jazeera (ভাষা বদলানো যায়) | `http://localhost:1200/aljazeera/rss` |
| `/dw/rss/:channel?` | Deutsche Welle | `http://localhost:1200/dw/rss` |
| `/telegram/channel/:username/:routeParams?` | Telegram চ্যানেল (পাবলিক) | `http://localhost:1200/telegram/channel/durov` |
| `/instagram/:category/:key` | Instagram (category/key-এর আসল মান docs.rsshub.app-এ দেখে নিন) | `http://localhost:1200/instagram/user/instagram` |
| `/economist/:endpoint` | The Economist (endpoint = সাইটের সেকশন) | `http://localhost:1200/economist/latest` |
| `/nytimes/rss/:cat?` | New York Times | `http://localhost:1200/nytimes/rss` |
| `/theguardian/editorial` | The Guardian সম্পাদকীয় | `http://localhost:1200/theguardian/editorial` |

## ব্যবহার

```bash
# 1. সার্ভার চালু করুন
docker compose up -d

# 2. ব্রাউজারে খুলে দেখুন (সার্ভার ঠিক আছে কি না)
curl http://localhost:1200/healthz

# 3. যেকোনো route আপনার RSS রিডারে (FreshRSS / NewsBlur / Miniflux) যোগ করুন
#    উদাহরণ: http://localhost:1200/bbc
#    অথবা পাবলিক ডেমো: https://rsshub.app/bbc (নিজের সার্ভার না থাকলে)
```

## নতুন route খুঁজতে চাইলে

1. https://docs.rsshub.app খুলুন (ব্রাউজারে — curl-কে 403 দেয়)।
2. অথবা সোর্সে দেখুন: `https://github.com/DIYgod/RSSHub/tree/master/lib/routes/`
   — প্রতিটি ফোল্ডারের নামই একেকটা route-এর namespace, আর `.ts` ফাইলের
   `path:` লাইনেই আসল route pattern লেখা থাকে।
