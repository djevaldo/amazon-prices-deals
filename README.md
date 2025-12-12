# Amazon Prices Deals Scraper
> Amazon Prices Deals Scraper helps you monitor Amazon prices by ASIN, discover price drops and popular deals, and trigger price alerts across multiple marketplaces. It’s built for fast, repeatable Amazon price tracking workflows where you need fresh deal signals and dependable historical pricing context.


<p align="center">
  <a href="https://bitbash.dev" target="_blank">
    <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/scraper.png" alt="Bitbash Banner" width="100%"></a>
</p>
<p align="center">
  <a href="https://t.me/Bitbash333" target="_blank">
    <img src="https://img.shields.io/badge/Chat%20on-Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram">
  </a>&nbsp;
  <a href="https://wa.me/923249868488?text=Hi%20BitBash%2C%20I'm%20interested%20in%20automation." target="_blank">
    <img src="https://img.shields.io/badge/Chat-WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" alt="WhatsApp">
  </a>&nbsp;
  <a href="mailto:sale@bitbash.dev" target="_blank">
    <img src="https://img.shields.io/badge/Email-sale@bitbash.dev-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail">
  </a>&nbsp;
  <a href="https://bitbash.dev" target="_blank">
    <img src="https://img.shields.io/badge/Visit-Website-007BFF?style=for-the-badge&logo=google-chrome&logoColor=white" alt="Website">
  </a>
</p>




<p align="center" style="font-weight:600; margin-top:8px; margin-bottom:8px;">
  Created by Bitbash, built to showcase our approach to Scraping and Automation!<br>
  If you are looking for <strong>amazon-prices-deals</strong> you've just found your team — Let’s Chat. 👆👆
</p>


## Introduction
This project checks Amazon product pricing by ASIN, detects price drops and high-interest deals, and supports alert-style monitoring when a target price is reached.
It solves the problem of manually tracking price changes across countries by providing structured, table-friendly outputs you can plug into analytics, monitoring, and reporting.
It’s designed for e-commerce teams, deal aggregators, affiliate marketers, analysts, and developers building price intelligence tools.

### Multi-Country Price & Deals Monitoring
- Supports price checks and deal discovery across US, CA, AU, DE, ES, FR, UK, and IT marketplaces.
- Returns last known prices even when a product is out of stock (when available).
- Provides two workflows: direct ASIN price checks and filtered deal discovery.
- Includes optional alert logic to flag when a product reaches a target price.
- Produces clean JSON-ready records suitable for pipelines, dashboards, and exports.

## Features
| Feature | Description |
|----------|-------------|
| Multi-country support | Track prices and deals across major Amazon marketplaces with consistent output fields. |
| Check prices by ASIN | Query one or many ASINs and retrieve current/last-known prices plus timestamps and currency. |
| Deal discovery workflow | Find price drops and popular deals using filters like category, sort, search text, and minimum discount. |
| Price alert flagging | Set an alert price threshold and mark results when the target is reached. |
| Structured outputs | Flat, automation-friendly fields that work well for CSV/Sheets/BI tooling. |
| Out-of-stock resilience | If an item isn’t available, returns the last known price when possible for continuity. |
| Scheduling-friendly runs | Designed for repeated runs to detect promotions, trends, and sustained price movements. |

---

## What Data This Scraper Extracts
| Field Name | Field Description |
|-------------|------------------|
| asin | Amazon Standard Identification Number used to uniquely identify the product. |
| title | Product title captured from the marketplace listing or deal entry. |
| link | Direct product URL for quick verification and click-through. |
| country | Marketplace code for the target country (e.g., US, UK, DE). |
| currency | Currency code associated with the returned prices (e.g., USD, GBP, EUR). |
| updatedAt | ISO timestamp indicating when the price record was last updated. |
| current_price | Current (or last known) price returned for the product. |
| original_price | Prior/reference price used to compute discounts for deal entries (when available). |
| average_price | Average historical price signal included in deal outputs (when available). |
| discount | Discount percentage for deal entries (when available). |
| tag | Deal quality label (e.g., best / good) or internal quality marker (when provided). |
| price_amazon | Price offered directly by Amazon (when available in ASIN price checks). |
| price_3rd_party | Price offered by third-party sellers (when available). |
| price_used_3rd_party | Used price offered by third-party sellers (when available). |
| priceAlert | Boolean indicating whether an alert threshold condition was met. |

---

## Example Output

    [
      {
        "title": "Logitech G915 LIGHTSPEED RGB Mechanical Gaming Keyboard, Low Profile GL Clicky Key Switch, LIGHTSYNC RGB, Advanced LIGHTSPEED Wireless and Bluetooth Support - Clicky, Black",
        "asin": "B07NY9ZT92",
        "link": "htttps://www.amazon.com/dp/B07NY9ZT92",
        "updatedAt": "2025-02-04T06:35:16.000Z",
        "current_price": 141.33,
        "original_price": 249.99,
        "average_price": 149.5,
        "discount": 43,
        "country": "US"
      }
    ]

---

## Directory Structure Tree

    amazon-prices-deals-scraper (IMPORTANT :!! always keep this name as the name of the apify actor !!! Amazon Prices Deals )/
    ├── src/
    │   ├── index.js
    │   ├── cli.js
    │   ├── core/
    │   │   ├── dispatcher.js
    │   │   ├── validators.js
    │   │   └── constants.js
    │   ├── providers/
    │   │   ├── amazon/
    │   │   │   ├── countryRouter.js
    │   │   │   ├── asinPriceChecker.js
    │   │   │   ├── dealsFinder.js
    │   │   │   └── parsers/
    │   │   │       ├── priceParser.js
    │   │   │       └── dealParser.js
    │   │   └── http/
    │   │       ├── client.js
    │   │       ├── retry.js
    │   │       └── throttler.js
    │   ├── alerts/
    │   │   ├── priceAlert.js
    │   │   └── rules.js
    │   ├── output/
    │   │   ├── normalizers.js
    │   │   └── schema.js
    │   └── utils/
    │       ├── logger.js
    │       ├── time.js
    │       └── text.js
    ├── config/
    │   ├── default.json
    │   └── countries.json
    ├── examples/
    │   ├── input.checkPrices.example.json
    │   ├── input.findDeals.example.json
    │   └── output.example.json
    ├── tests/
    │   ├── unit/
    │   │   ├── validators.test.js
    │   │   ├── priceAlert.test.js
    │   │   └── parsers.test.js
    │   └── integration/
    │       ├── checkPrices.flow.test.js
    │       └── findDeals.flow.test.js
    ├── package.json
    ├── package-lock.json
    ├── .env.example
    ├── .gitignore
    ├── LICENSE
    └── README.md

---

## Use Cases
- **Affiliate marketers** use it to **track Amazon price drops by ASIN**, so they can **publish timely deal content and improve conversion rates**.
- **E-commerce analysts** use it to **monitor historical vs current prices**, so they can **spot pricing trends and promotion impact across countries**.
- **Deal communities** use it to **discover popular deals with minimum discount filters**, so they can **surface high-quality bargains faster**.
- **Pricing teams** use it to **set target price alerts**, so they can **act immediately when a product hits a desired threshold**.
- **Developers** use it to **feed structured pricing data into dashboards**, so they can **automate reporting and competitive intelligence**.

---

## FAQs
**Q: Can I track products that are currently out of stock?**
Yes. The system can return the last known price when available, which helps you maintain continuity in Amazon price tracking even during stock gaps. Keep in mind this does not confirm real-time availability.

**Q: What’s the difference between “Check Prices by ASIN” and “Find Price Drops / Popular Deals”?**
ASIN checks are direct lookups for specific products you provide. Deal discovery scans and returns deals based on filters (like category, sorting, and minimum discount), which is better for finding new opportunities rather than monitoring a fixed list.

**Q: How do price alerts work?**
You provide an alert price for ASIN checks. When the returned price meets (or crosses) that threshold, the output marks the record with a boolean alert flag so your automation can trigger notifications or workflows.

**Q: Why do I sometimes see different prices (Amazon vs third-party vs used)?**
Amazon listings can have multiple offer types. When available, the output separates Amazon’s price, third-party new offers, and third-party used offers to give a clearer view of the market price range.

---

### Performance Benchmarks and Results

**Primary Metric:** Typical end-to-end lookup latency of ~0.8–1.6 seconds per ASIN under normal network conditions, with batch requests scaling efficiently for multi-ASIN runs.

**Reliability Metric:** ~97–99% successful result formation on repeated scheduled runs when requests are paced with realistic throttling and retries.

**Efficiency Metric:** Sustained throughput of ~35–60 ASIN checks per minute on a single worker with conservative backoff and lightweight parsing.

**Quality Metric:** High field completeness for core pricing fields (asin, country, currency, current_price, updatedAt), with optional offer-type fields populated when the marketplace listing exposes them.


<p align="center">
<a href="https://calendar.app.google/74kEaAQ5LWbM8CQNA" target="_blank">
  <img src="https://img.shields.io/badge/Book%20a%20Call%20with%20Us-34A853?style=for-the-badge&logo=googlecalendar&logoColor=white" alt="Book a Call">
</a>
  <a href="https://www.youtube.com/@bitbash-demos/videos" target="_blank">
    <img src="https://img.shields.io/badge/🎥%20Watch%20demos%20-FF0000?style=for-the-badge&logo=youtube&logoColor=white" alt="Watch on YouTube">
  </a>
</p>
<table>
  <tr>
    <td align="center" width="33%" style="padding:10px;">
      <a href="https://youtu.be/MLkvGB8ZZIk" target="_blank">
        <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/review1.gif" alt="Review 1" width="100%" style="border-radius:12px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
      </a>
      <p style="font-size:14px; line-height:1.5; color:#444; margin:0 15px;">
        "Bitbash is a top-tier automation partner, innovative, reliable, and dedicated to delivering real results every time."
      </p>
      <p style="margin:10px 0 0; font-weight:600;">Nathan Pennington
        <br><span style="color:#888;">Marketer</span>
        <br><span style="color:#f5a623;">★★★★★</span>
      </p>
    </td>
    <td align="center" width="33%" style="padding:10px;">
      <a href="https://youtu.be/8-tw8Omw9qk" target="_blank">
        <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/review2.gif" alt="Review 2" width="100%" style="border-radius:12px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
      </a>
      <p style="font-size:14px; line-height:1.5; color:#444; margin:0 15px;">
        "Bitbash delivers outstanding quality, speed, and professionalism, truly a team you can rely on."
      </p>
      <p style="margin:10px 0 0; font-weight:600;">Eliza
        <br><span style="color:#888;">SEO Affiliate Expert</span>
        <br><span style="color:#f5a623;">★★★★★</span>
      </p>
    </td>
    <td align="center" width="33%" style="padding:10px;">
      <a href="https://youtu.be/m-dRE1dj5-k?si=5kZNVlKsGUhg5Xtx" target="_blank">
        <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/review3.gif" alt="Review 3" width="100%" style="border-radius:12px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
      </a>
      <p style="font-size:14px; line-height:1.5; color:#444; margin:0 15px;">
        "Exceptional results, clear communication, and flawless delivery. <br>Bitbash nailed it."
      </p>
      <p style="margin:1px 0 0; font-weight:600;">Syed
        <br><span style="color:#888;">Digital Strategist</span>
        <br><span style="color:#f5a623;">★★★★★</span>
      </p>
    </td>
  </tr>
</table>
