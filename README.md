# Awesome APIs for Students [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of **free public APIs** perfect for student projects, capstones, thesis work, and learning to code — with **code examples in JavaScript, PHP, Python, C# / .NET, Go, and Java**.

Most "awesome APIs" lists are huge dumps that overwhelm a student trying to ship their first weather app. This list is opinionated: every API here is **free or has a generous free tier**, **doesn't require a credit card to start**, and is **suitable for a student project you can finish in a weekend**.

For each category, you'll find code samples in multiple languages so you can plug them into whatever you're learning — whether that's a Laravel app, a .NET MVC project, a React frontend, or a Python notebook.

---

## Contents

- [Legend](#legend)
- [Quick Start by Language](#quick-start-by-language)
- [APIs by Category](#apis-by-category)
  - [☁️ Weather](#weather)
  - [🗺️ Geocoding & Maps](#geocoding--maps)
  - [💱 Currency & Finance](#currency--finance)
  - [📰 News](#news)
  - [⚽ Sports](#sports)
  - [🍕 Food & Recipes](#food--recipes)
  - [🎬 Entertainment & Media](#entertainment--media)
  - [📚 Education & Books](#education--books)
  - [🤖 AI & Machine Learning](#ai--machine-learning)
  - [🏛️ Government & Open Data](#government--open-data)
  - [🇵🇭 Philippines-Specific](#philippines-specific)
  - [🎲 Random & Fun](#random--fun)
  - [🛠️ Developer Tools & Utilities](#developer-tools--utilities)
- [Project Ideas](#project-ideas)
- [HTTP Client Cheat Sheet](#http-client-cheat-sheet)
- [Contributing](#contributing)
- [License](#license)

---

## Legend

| Symbol | Meaning |
|---|---|
| 🆓 | No authentication required — just `fetch()` and go |
| 🔑 | Free API key required (no credit card) |
| 💳 | Free tier exists but credit card or paid plan available |
| 🏆 | Recommended for first-time API users |

---

## Quick Start by Language

How to call a JSON API in each major student language. Examples use the wttr.in weather API (no key needed).

### JavaScript (Browser / Node.js)

```js
const res = await fetch("https://wttr.in/Manila?format=j1");
const data = await res.json();
console.log(data.current_condition[0].temp_C);
```

### PHP

```php
<?php
$json = file_get_contents("https://wttr.in/Manila?format=j1");
$data = json_decode($json, true);
echo $data["current_condition"][0]["temp_C"];
```

With Guzzle (Laravel / modern PHP):

```php
use GuzzleHttp\Client;
$client = new Client();
$response = $client->get("https://wttr.in/Manila?format=j1");
$data = json_decode($response->getBody(), true);
echo $data["current_condition"][0]["temp_C"];
```

### Python

```python
import requests
r = requests.get("https://wttr.in/Manila?format=j1")
data = r.json()
print(data["current_condition"][0]["temp_C"])
```

### C# / .NET

```csharp
using System.Net.Http;
using System.Text.Json;

var client = new HttpClient();
var json = await client.GetStringAsync("https://wttr.in/Manila?format=j1");
var doc = JsonDocument.Parse(json);
var temp = doc.RootElement
    .GetProperty("current_condition")[0]
    .GetProperty("temp_C").GetString();
Console.WriteLine(temp);
```

### Go

```go
package main

import (
    "encoding/json"
    "fmt"
    "net/http"
)

func main() {
    resp, _ := http.Get("https://wttr.in/Manila?format=j1")
    defer resp.Body.Close()
    var data map[string]interface{}
    json.NewDecoder(resp.Body).Decode(&data)
    cond := data["current_condition"].([]interface{})[0].(map[string]interface{})
    fmt.Println(cond["temp_C"])
}
```

### Java

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

HttpClient client = HttpClient.newHttpClient();
HttpRequest req = HttpRequest.newBuilder()
    .uri(URI.create("https://wttr.in/Manila?format=j1"))
    .build();
HttpResponse<String> res = client.send(req, HttpResponse.BodyHandlers.ofString());
System.out.println(res.body());
```

---

## APIs by Category

### Weather

- 🆓🏆 **[wttr.in](https://wttr.in)** — Get the weather for any city as JSON, plain text, or ASCII art. No API key, no signup, just `https://wttr.in/Manila?format=j1`.
- 🔑🏆 **[OpenWeatherMap](https://openweathermap.org/api)** — Free tier: 1,000 calls/day. Current weather, forecast, historical data. The default choice for weather projects.
- 🔑 **[WeatherAPI.com](https://www.weatherapi.com/)** — Free tier: 1M calls/month. More generous than OpenWeatherMap.
- 🆓 **[Open-Meteo](https://open-meteo.com/)** — Free non-commercial weather API. No key required, includes forecasts and historical data.
- 🆓 **[7Timer!](http://www.7timer.info/doc.php)** — Free weather forecast for stargazing, civil aviation, agriculture.

### Geocoding & Maps

- 🆓🏆 **[Nominatim (OpenStreetMap)](https://nominatim.org/release-docs/develop/api/Overview/)** — Free geocoding and reverse geocoding. Be respectful — max 1 req/sec.
- 🔑 **[OpenCage Geocoding](https://opencagedata.com/)** — 2,500 free requests/day. Cleaner JSON than Nominatim.
- 🆓 **[REST Countries](https://restcountries.com/)** — Country info: capital, population, currencies, flags, languages.
- 🆓 **[IP-API](http://ip-api.com/)** — Free IP geolocation. 45 requests/minute. No key.
- 🆓 **[ipapi.co](https://ipapi.co/)** — IP-based geolocation. Free for 1,000 requests/day.
- 🔑 **[Mapbox](https://www.mapbox.com/)** — 50,000 map loads/month free. Maps, geocoding, directions, isochrones.

### Currency & Finance

- 🔑🏆 **[ExchangeRate-API](https://www.exchangerate-api.com/)** — 1,500 currency requests/month free. Reliable.
- 🆓 **[Frankfurter](https://www.frankfurter.app/)** — Currency conversion using ECB data. No key, no limits documented.
- 🆓 **[CoinGecko](https://www.coingecko.com/en/api)** — Free crypto API: prices, market cap, history. 10-30 calls/minute.
- 🔑 **[Polygon.io](https://polygon.io/)** — Stock market data. Free tier: 5 API calls/min.
- 🔑 **[Alpha Vantage](https://www.alphavantage.co/)** — Stocks, forex, crypto. 25 requests/day free.
- 🔑 **[Finnhub](https://finnhub.io/)** — Stocks and economic data. 60 calls/minute free.

### News

- 🔑🏆 **[NewsAPI](https://newsapi.org/)** — Free for development: 100 requests/day. Headlines from 80,000+ sources.
- 🆓 **[GNews](https://gnews.io/)** — 100 requests/day free.
- 🆓 **[The Guardian Open Platform](https://open-platform.theguardian.com/)** — Generous free tier with full article content.
- 🆓 **[Reddit JSON API](https://www.reddit.com/dev/api)** — Append `.json` to any Reddit URL — instant JSON. No auth for read.
- 🆓 **[Hacker News API](https://github.com/HackerNews/API)** — Stories, comments, users. No key.

### Sports

- 🆓🏆 **[TheSportsDB](https://www.thesportsdb.com/api.php)** — Football, basketball, NFL, esports. Free tier with key `3`.
- 🆓 **[Football-data.org](https://www.football-data.org/)** — Football fixtures and standings. 10 calls/minute free.
- 🆓 **[NBA Stats (unofficial)](https://github.com/swar/nba_api)** — Wraps the official NBA endpoints.
- 🔑 **[API-Football](https://www.api-football.com/)** — 100 requests/day free.

### Food & Recipes

- 🆓🏆 **[TheMealDB](https://www.themealdb.com/api.php)** — Free recipes, ingredients, categories. Test key `1`.
- 🆓 **[TheCocktailDB](https://www.thecocktaildb.com/api.php)** — Cocktail recipes from the same maintainer as TheMealDB.
- 🔑 **[Spoonacular](https://spoonacular.com/food-api)** — 150 requests/day free. Recipe search, nutrition, meal planning.
- 🆓 **[Open Food Facts](https://world.openfoodfacts.org/data)** — Crowdsourced food product database. Scan a barcode, get the data.
- 🆓 **[Edamam Recipe Search](https://developer.edamam.com/edamam-recipe-api)** — 5 requests/minute free.

### Entertainment & Media

- 🔑🏆 **[TMDB (The Movie DB)](https://developer.themoviedb.org/)** — Movies, TV shows, cast, posters. Generous free tier — the go-to for movie apps.
- 🆓 **[OMDb](http://www.omdbapi.com/)** — Movie info via title search. 1,000 requests/day free.
- 🆓 **[Jikan (MyAnimeList)](https://jikan.moe/)** — Anime and manga data. No key, rate-limited.
- 🆓 **[AniList GraphQL](https://anilist.co/graphql)** — GraphQL API for anime/manga.
- 🆓 **[Spotify Web API](https://developer.spotify.com/documentation/web-api)** — Music metadata, playlists. Requires OAuth but free.
- 🆓 **[Deezer](https://developers.deezer.com/api)** — Music tracks, artists, albums. No auth for public data.
- 🆓 **[Giphy](https://developers.giphy.com/)** — GIFs. Free with API key.
- 🆓 **[Pexels](https://www.pexels.com/api/)** — Free stock photos and videos. Free with API key.
- 🆓 **[Unsplash](https://unsplash.com/developers)** — High-quality free photos. 50 requests/hour on demo tier.

### Education & Books

- 🆓🏆 **[Open Library](https://openlibrary.org/developers/api)** — Books, authors, covers. No key. Great for library apps.
- 🆓 **[Google Books](https://developers.google.com/books)** — Search 40M+ books. Free.
- 🆓 **[Project Gutenberg (Gutendex)](https://gutendex.com/)** — 70,000+ free ebooks via JSON API.
- 🆓 **[Numbers API](http://numbersapi.com/)** — Trivia, math, date facts about any number.
- 🆓 **[Dictionary API](https://dictionaryapi.dev/)** — Free English dictionary with definitions, examples, audio.
- 🆓 **[Wikipedia REST API](https://en.wikipedia.org/api/rest_v1/)** — Search Wikipedia, get summaries, page HTML.
- 🆓 **[CollegeFootballData](https://collegefootballdata.com/)** — College football stats and games.

### AI & Machine Learning

- 💳🏆 **[Hugging Face Inference API](https://huggingface.co/docs/api-inference/index)** — Free tier for many models: text gen, classification, image gen.
- 💳 **[Google Gemini API](https://ai.google.dev/)** — Generous free tier for text + multimodal models.
- 💳 **[Groq](https://groq.com/)** — Free tier with very fast inference on Llama / Mixtral models.
- 💳 **[OpenAI](https://platform.openai.com/)** — Pay as you go, $5 free credit on signup (subject to change).
- 💳 **[Anthropic Claude API](https://www.anthropic.com/api)** — High-quality models with a free trial.
- 🆓 **[Cloudflare Workers AI](https://developers.cloudflare.com/workers-ai/)** — Free quota of LLM/image inference.
- 🆓 **[DeepL Translate](https://www.deepl.com/pro-api)** — 500,000 chars/month free. Higher quality than Google Translate for many language pairs.

### Government & Open Data

- 🆓 **[NASA Open APIs](https://api.nasa.gov/)** — Astronomy Picture of the Day (APOD), Mars rover photos, asteroids. Demo key works for testing.
- 🆓 **[USGS Earthquake](https://earthquake.usgs.gov/fdsnws/event/1/)** — Real-time and historical earthquake data.
- 🆓 **[Data.gov](https://www.data.gov/)** — US government open datasets across hundreds of agencies.
- 🆓 **[World Bank Open Data](https://data.worldbank.org/)** — Country-level economic indicators.
- 🆓 **[WHO GHO](https://www.who.int/data/gho)** — World Health Organization global health observatory data.

### Philippines-Specific

- 🆓 **[PSGC API](https://psgc.gitlab.io/api/)** — Philippine Standard Geographic Code: regions, provinces, cities, barangays. Essential for any PH address form.
- 🆓 **[Bangko Sentral ng Pilipinas (BSP) Reference Exchange Rates](https://www.bsp.gov.ph/SitePages/Statistics/ExchangeRate.aspx)** — Official PHP exchange rates.
- 🆓 **[PAGASA Weather](https://www.pagasa.dost.gov.ph/)** — Philippine weather and typhoon tracking (scrape-friendly RSS / data feeds).
- 🆓 **[Phividec / DOST APIs](https://www.dost.gov.ph/)** — Various PH government datasets.

### Random & Fun

- 🆓🏆 **[JSONPlaceholder](https://jsonplaceholder.typicode.com/)** — Fake REST API for testing and prototyping. The first API every student should hit.
- 🆓 **[Pokémon API](https://pokeapi.co/)** — All Pokémon data ever. Most popular learning API on GitHub.
- 🆓 **[Star Wars API (SWAPI)](https://swapi.tech/)** — Star Wars films, characters, planets.
- 🆓 **[Rick and Morty API](https://rickandmortyapi.com/)** — Characters, episodes, locations.
- 🆓 **[Dog API](https://dog.ceo/dog-api/)** — Random dog images by breed.
- 🆓 **[Cat Facts](https://catfact.ninja/)** — Random cat facts.
- 🆓 **[Bored API](https://bored-api.appbrewery.com/)** — Get a random activity to do when bored.
- 🆓 **[Advice Slip](https://api.adviceslip.com/)** — Random advice. One endpoint, no key.
- 🆓 **[Joke API](https://jokeapi.dev/)** — Programming, dark, pun jokes.
- 🆓 **[Quotable](https://github.com/lukePeavey/quotable)** — Famous quotes API.
- 🆓 **[uselessfacts](https://uselessfacts.jsph.pl/)** — Random useless facts.

### Developer Tools & Utilities

- 🆓 **[GitHub REST API](https://docs.github.com/en/rest)** — Repos, issues, users. 60 requests/hour unauthed, 5,000 with token.
- 🆓 **[GitLab API](https://docs.gitlab.com/ee/api/)** — Same idea for GitLab projects.
- 🆓 **[QR Code Generator](https://goqr.me/api/)** — Generate QR codes via URL. No key.
- 🆓 **[QR Code Monkey API](https://www.qrcode-monkey.com/qr-code-api-with-logo/)** — Higher-quality QR codes with logo support.
- 🆓 **[Have I Been Pwned](https://haveibeenpwned.com/API/v3)** — Check if an email has been in a breach. (Some endpoints require key now.)
- 🆓 **[is.gd / TinyURL](https://is.gd/developers.php)** — URL shortener APIs.
- 🆓 **[Public Holidays](https://date.nager.at/Api)** — Public holidays for 100+ countries by year.
- 🆓 **[Worldtime API](http://worldtimeapi.org/)** — Current time and timezone for any city.
- 🆓 **[ipify](https://www.ipify.org/)** — Get the caller's public IP. One endpoint.
- 🆓 **[picsum.photos](https://picsum.photos/)** — Lorem Ipsum for images. `https://picsum.photos/300/200` returns a random 300x200 image.
- 🆓 **[Robohash](https://robohash.org/)** — Generate unique robot avatars from any string.
- 🆓 **[DiceBear Avatars](https://www.dicebear.com/)** — Generate avatars from initials, identicons, etc.

---

## Project Ideas

If you're staring at a blank IDE wondering what to build, here are projects sized for a weekend, a semester, or a capstone — each pairs naturally with APIs from this list.

### Weekend Projects

1. **Weather Dashboard** — Open-Meteo + your city. Show today's forecast with icons.
2. **Crypto Tracker** — CoinGecko. Track your favorite coins with portfolio totals.
3. **Movie Watchlist** — TMDB. Search movies, save to a local watchlist.
4. **Recipe Finder** — TheMealDB. Find recipes by ingredients you have.
5. **Pomodoro + Random Quote** — Quotable. New motivational quote at every break.
6. **QR Code Generator for Class** — goqr.me. Generate attendance QR codes.
7. **Currency Converter** — Frankfurter. Multi-currency converter for your barangay shop.
8. **Pokédex Clone** — PokeAPI. Search and view Pokémon with stats.
9. **Random Workout Generator** — Bored API + custom logic.
10. **Birthday Reminder with Astronomy Pic** — NASA APOD shows the picture from someone's birthday.

### Semester / Group Project

11. **Internet Cafe Reservation System** — show available PC stations + per-hour rates with QR code check-in.
12. **Event Locator** — Nominatim + REST Countries to map and filter events.
13. **PSGC-Powered Address Form** — Use PSGC API for proper Philippine address dropdowns (region → province → city → barangay).
14. **Earthquake Alert System** — USGS + email/SMS notifications for nearby quakes.
15. **News Aggregator with Sentiment** — NewsAPI + Hugging Face sentiment classifier.
16. **Online Library Catalog** — Open Library + Google Books for ISBN lookup.
17. **Recipe + Nutrition Tracker** — Spoonacular for recipes, log to your DB.
18. **AI Chatbot with Context** — Groq or Gemini, with chat history saved to MySQL.
19. **Anime Recommendation Engine** — Jikan + simple content-based filtering.
20. **OFW Remittance Calculator** — ExchangeRate-API + BSP rates for accurate PHP conversions.

### Capstone-Worthy

21. **Disaster Information Hub** — Combine USGS, PAGASA, WHO, and news APIs for a regional emergency dashboard.
22. **Smart Cafe POS with AI Ordering** — POS integrated with Spoonacular + a Groq chatbot for menu recommendations.
23. **Multi-LLM Chat Studio** — One UI, switchable backends (Gemini, Groq, Claude, OpenAI). Compare outputs side by side.
24. **Local Business Directory with Maps** — Mapbox + custom DB + reviews.
25. **Vaccination Record System** — WHO API for reference data + your own immunization tracking schema.
26. **Esports Tournament Tracker** — TheSportsDB + scrapers for local tournaments.

---

## HTTP Client Cheat Sheet

What to install in each language to make API calls cleanly.

### JavaScript / Node.js

```
# Built-in fetch in modern Node and browsers — no install needed.
# For React: just use fetch or axios
npm install axios
```

### PHP

```
# Built-in: file_get_contents() and curl_*
# Modern: Guzzle
composer require guzzlehttp/guzzle

# Laravel: built-in HTTP client
use Illuminate\Support\Facades\Http;
$response = Http::get("https://wttr.in/Manila?format=j1");
```

### Python

```
pip install requests        # most common
pip install httpx           # async-friendly modern alternative
```

### C# / .NET

```
# HttpClient is built-in (System.Net.Http)
# For nicer API: install RestSharp
dotnet add package RestSharp
# Or Refit for typed HTTP clients
dotnet add package Refit
```

### Go

```
// Built-in net/http is enough for most cases.
// Popular wrapper: resty
go get github.com/go-resty/resty/v2
```

### Java

```
// Built-in java.net.http.HttpClient (Java 11+)
// Popular wrapper: OkHttp
implementation 'com.squareup.okhttp3:okhttp:4.12.0'

// Spring Boot: WebClient or RestTemplate
```

### Frameworks Worth Knowing

- **PHP**: Laravel (full-stack), Symfony (enterprise), CodeIgniter (lightweight), Slim (microframework).
- **C# / .NET**: ASP.NET Core MVC, ASP.NET Core Web API, Blazor (full-stack with C#), Minimal APIs.
- **JavaScript**: Express (Node), Next.js (React), NestJS (Angular-style), SvelteKit, Astro.
- **Python**: Django (full-stack), Flask (micro), FastAPI (async APIs).
- **Go**: Gin, Echo, Fiber, Chi.
- **Java**: Spring Boot, Quarkus, Micronaut.

---


- 🆓 **[ChuckNorris.io](https://api.chucknorris.io/)** — Random Chuck Norris jokes, no auth, perfect for first-API tutorials.


- 🆓 **[icanhazdadjoke](https://icanhazdadjoke.com/api)** — Wholesome dad jokes API. Set Accept header to application/json.


- 🆓 **[Studio Ghibli API](https://ghibliapi.vercel.app/)** — Films, characters, locations from Studio Ghibli. Great for movie list demos.


- 🔑 **[The One API (Lord of the Rings)](https://the-one-api.dev/)** — Books, movies, characters, quotes from LotR. Free with key.


- 🆓 **[Disney API](https://disneyapi.dev/)** — Search Disney characters, films, TV shows. No auth.


- 🔑 **[Marvel API](https://developer.marvel.com/)** — Comics, characters, creators. Free tier with key.


- 🔑 **[RAWG Video Games](https://rawg.io/apidocs)** — Largest video game database. Free tier 20k requests/month.


- 🆓 **[ZenQuotes](https://zenquotes.io/)** — Random inspirational quotes. Excellent for first API project.


- 🆓 **[Yes No](https://yesno.wtf/api)** — Yes/no oracle with a GIF. Single endpoint, fun for binary decisions.


- 🆓 **[Datamuse](https://www.datamuse.com/api/)** — Word-finding query engine: rhymes, synonyms, related words. No auth.


- 🆓 **[Time API](https://timeapi.io/swagger/index.html)** — Current time in any timezone, time conversion. Free.


- 🆓 **[ShrtCo](https://shrtco.de/docs)** — Free URL shortener API. No auth, simple JSON response.

## Contributing

Pull requests welcome! See [contributing.md](contributing.md). Add APIs that are:

- Free or have a generous free tier with no credit card required
- Suitable for student projects (good docs, reasonable rate limits)
- Active and maintained (last update within the last 2 years)

Add language code samples for popular APIs to help students from any language background.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, [Charlie James Zapico Abejo](https://github.com/CharlieJamesGwapo) has waived all copyright and related or neighboring rights to this work.

---

<p align="center">
<i>Built by a student, for students. If this list helped you ship something, consider starring the repo so other students can find it. ⭐</i>
</p>
