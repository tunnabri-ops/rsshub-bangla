# RSSHub Bangla — সবকিছু RSS করুন

Bangla-ready RSSHub setup, built on **DIYgod/RSSHub**.

- **Original repo:** https://github.com/DIYgod/RSSHub (Everything is RSSible — ৫,০০০+ পাবলিক ইনস্ট্যান্সের RSS নেটওয়ার্ক)

## কী আছে / What is inside

- `docker-compose.yml` — নিজের RSSHub সার্ভার: `diygod/rsshub` ইমেজ, পোর্ট 1200, Redis ক্যাশ, `/healthz` হেলথচেক।
- `bangla-routes.md` — যাচাই করা RSSHub route-গুলোর তালিকা + একটা সত্যি কথা: RSSHub-এ বাংলা কোনো route নেই।

## যা ঠিক করা হয়েছে / What was fixed

- Upstream-এর compose-এ browserless (Playwright) সার্ভিসও আছে — JS-ভারী route ছাড়া সেটা দরকার হয় না, তাই এই compose সহজ রাখা হয়েছে (rsshub + redis)। দরকার হলে upstream compose থেকে browserless যোগ করে নিন।
- Upstream docs-এ হাজারো route — কোনটা আসল, কোনটা বাংলা কাজে লাগবে, বোঝা কঠিন। `bangla-routes.md`-এ শুধু সোর্স থেকে যাচাই করা route আছে, আর স্পষ্ট লেখা আছে RSSHub বাংলা খবর দেয় না — বাংলা ফিডের জন্য সরাসরি RSS ব্যবহার করুন (`newsblur-bangla/bangla-feeds.opml`)।

## ব্যবহার / How to use

```bash
# 1. সার্ভার চালু করুন
docker compose up -d

# 2. ঠিক আছে কি না দেখুন
curl http://localhost:1200/healthz

# 3. ব্রাউজারে খুলুন, যেমন: http://localhost:1200/bbc
#    অথবা আপনার RSS রিডারে যোগ করুন
```

Route-এর পুরো তালিকা `bangla-routes.md`-এ।
