# VibeCode Semantic Versioning

> *"It's not a bug, it's discipline."*

---

## The Question

You may have noticed our version numbers appear... unconventional:

| Year | Version | User |
|------|---------|------|
| 2003 | v0.0.1 | Elizabeth Holmes |
| 2015 | v0.0.9 | Diddy |
| 2016 | v0.0.7 | Stefan Qin |
| 2017 | v0.2 | Alex Mashinsky |
| 2018 (Jan) | v0.0.3 | Trevor Milton |
| 2018 (Mar) | v0.1 | Mike Hughes |
| 2019 | v0.1.2 | SBF |
| 2021 | v0.1.5 | Logan Paul |

**"This makes no sense!"** you cry. **"v0.0.9 comes before v0.0.3? v0.2 jumps from v0.0.7?"**

---

## The Answer

We learned versioning from the best.

---

## Microsoft Windows Version History

| Year | Version | "Internal" Version | Notes |
|------|---------|--------------------|-------|
| 1985 | [1.0](https://en.wikipedia.org/wiki/Windows_1.0) | 1.0 | The beginning |
| 1987 | [2.0](https://en.wikipedia.org/wiki/Windows_2.0) | 2.0 | Logical |
| 1990 | [3.0](https://en.wikipedia.org/wiki/Windows_3.0) | 3.0 | Still logical |
| 1992 | [3.1](https://en.wikipedia.org/wiki/Windows_3.1) | 3.1 | Minor bump |
| 1993 | [3.11](https://en.wikipedia.org/wiki/Windows_3.1x) | 3.11 | For Workgroups |
| 1993 | [NT 3.1](https://en.wikipedia.org/wiki/Windows_NT_3.1) | NT 3.1 | Wait, 3.1 again? |
| 1994 | [NT 3.5](https://en.wikipedia.org/wiki/Windows_NT_3.5) | NT 3.5 | Now there's two tracks |
| 1995 | [**95**](https://en.wikipedia.org/wiki/Windows_95) | 4.0 | 3.11 → 95. Normal. |
| 1996 | [NT 4.0](https://en.wikipedia.org/wiki/Windows_NT_4.0) | NT 4.0 | Different track |
| 1998 | [**98**](https://en.wikipedia.org/wiki/Windows_98) | 4.10 | 95 → 98. Year-based now? |
| 2000 | [**2000**](https://en.wikipedia.org/wiki/Windows_2000) | NT 5.0 | Millennium vibes |
| 2000 | [**ME**](https://en.wikipedia.org/wiki/Windows_ME) | 4.90 | Millennium Edition. Same year as 2000. |
| 2001 | [**XP**](https://en.wikipedia.org/wiki/Windows_XP) | NT 5.1 | Letters now |
| 2007 | [**Vista**](https://en.wikipedia.org/wiki/Windows_Vista) | NT 6.0 | Full words |
| 2009 | [**7**](https://en.wikipedia.org/wiki/Windows_7) | NT 6.1 | Back to numbers |
| 2012 | [**8**](https://en.wikipedia.org/wiki/Windows_8) | NT 6.2 | Sequential |
| 2013 | [8.1](https://en.wikipedia.org/wiki/Windows_8.1) | NT 6.3 | Point release |
| 2015 | [**10**](https://en.wikipedia.org/wiki/Windows_10) | NT 10.0 | Skipped 9 entirely |
| 2021 | [**11**](https://en.wikipedia.org/wiki/Windows_11) | NT 10.0 | "10 is the last version" was a lie |

---

## The Pattern

```
1.0 → 2.0 → 3.0 → 3.1 → 3.11 → NT 3.1 → NT 3.5 → 95 → NT 4.0 → 98 → 2000 → ME → XP → Vista → 7 → 8 → 8.1 → 10 → 11
```

**Analysis:**
- Version 4 through 94? Skipped.
- Version 9? [Intentionally skipped](https://www.extremetech.com/computing/191279-why-is-it-called-windows-10-not-windows-9) because legacy code checked `if version.startswith("9")` to detect Windows 95/98.
- NT and consumer lines ran in parallel with different version numbers.
- Sometimes years, sometimes letters, sometimes vibes.

---

## VibeCode Version Philosophy

We follow the same discipline:

```
v0.0.1 → v0.0.9 → v0.0.7 → v0.2 → v0.0.3 → v0.1 → v0.1.2 → v0.1.5 → v9.2.1
```

**Why?**

1. **Parallel development tracks** - Different teams, different versions
2. **Customer-specific builds** - Enterprise clients got custom version numbers
3. **Marketing requirements** - v0.2 sounds more mature than v0.0.4
4. **Vibes** - Sometimes a version just *feels* right

---

## Version Selection Algorithm

```ruby
# version_selector.rb (v0.0.1 - STILL IN USE)
def next_version(current, context)
  case context[:vibe]
  when :enterprise
    bump_major(current)
  when :startup
    random_minor(current)
  when :fraud
    whatever_sounds_impressive(current)
  else
    current.succ  # Normal increment (rarely used)
  end
end

def whatever_sounds_impressive(current)
  [
    # Windows vibes
    "0.2", "1.0", "2.0", "95", "98", "2000", "ME", "XP", "Vista", "7", "8", "10", "11",

    # iPhone vibes (Roman numerals)
    "X", "XS", "XR", "XI", "XII", "XIII", "XIV", "XV",

    # Tier vibes
    "Pro", "Pro Max", "Ultra", "Enterprise", "Ultimate", "Home", "Starter",

    # Apple suffix vibes
    "SE", "Air", "Mini", "Plus", "Max", "Studio",

    # Tesla S3XY vibes
    "S", "3", "X", "Y", "Cybertruck", "Cybercab", "Roadster", "Semi",
    "Plaid", "Ludicrous", "Insane",

    # Xbox vibes (absolute chaos)
    "360", "One", "One S", "One X", "Series S", "Series X",

    # Android dessert vibes
    "Cupcake", "Donut", "Eclair", "Froyo", "Gingerbread", "Honeycomb",
    "Ice Cream Sandwich", "Jelly Bean", "KitKat", "Lollipop", "Marshmallow",
    "Nougat", "Oreo", "Pie", "Vanilla Ice Cream",

    # macOS vibes (big cats → California)
    "Cheetah", "Puma", "Jaguar", "Panther", "Tiger", "Leopard", "Snow Leopard",
    "Lion", "Mountain Lion", "Mavericks", "Yosemite", "El Capitan", "Sierra",
    "High Sierra", "Mojave", "Catalina", "Big Sur", "Monterey", "Ventura", "Sonoma",

    # Ubuntu vibes (adjective + animal)
    "Warty Warthog", "Hoary Hedgehog", "Breezy Badger", "Dapper Drake",
    "Noble Numbat", "Jammy Jellyfish",

    # USB vibes (the worst offender)
    "3.1 Gen 1", "3.1 Gen 2", "3.2 Gen 1", "3.2 Gen 2", "3.2 Gen 2x2", "4",

    # GPU vibes
    "GTX 1080", "RTX 2080", "RTX 3090", "RTX 4090", "Ti", "SUPER",

    # Intel vibes
    "i3", "i5", "i7", "i9", "Core Ultra", "Alder Lake", "Raptor Lake",

    # Bluetooth vibes
    "4.0 LE", "5.0", "5.3",

    # Star Wars release order vibes
    "Episode IV", "Episode V", "Episode VI", "Episode I", "Episode II", "Episode III",

    # VibeCode original: African mountains (because California is taken)
    "Kilimanjaro", "Atlas", "Drakensberg", "Rwenzori", "Simien", "Toubkal",
    "Kenya", "Meru", "Elgon", "Karisimbi",

    # VibeCode original: African cities (for enterprise editions)
    "Casablanca", "Marrakech", "Tangier", "Fes", "Agadir", "Rabat",
    "Lagos", "Nairobi", "Cape Town", "Johannesburg", "Cairo", "Addis Ababa",
    "Dakar", "Accra", "Tunis", "Algiers",

    # Great Firewall Edition™ (中国特供版)
    "长城", "Beijing", "Shanghai", "Shenzhen", "Hangzhou", "Chengdu",
    "Dragon", "Phoenix", "Jade", "Harmony", "Golden Shield",
    "Zhongguancun", "Pudong", "Tianhe",

    # Russian Federation Edition™ (Российская Федерация)
    "Kremlin", "Moscow", "Petersburg", "Siberia", "Sputnik", "Mir",
    "Ural", "Baikal", "Volga", "Taiga", "Matryoshka",
    "Skolkovo", "Yandex", "Kalashnikov"
  ].sample
end
```

---

## FAQ

**Q: Is this SemVer compliant?**
A: We use VibeSemVer™. It's compatible with SemVer if you squint.

**Q: How do I know which version is newer?**
A: Check the release date, not the version number.

**Q: Why not just use sequential versions?**
A: Where's the fun in that?

**Q: What version is Rust edition 2030?**
A: v9.2.1. Always v9.2.1. It's the version that fixes everything.

---

## Current Version

**Production:** v9.2.1 (Rust edition 2030)

**Legacy Ruby versions:** Deprecated. Court-ordered release only.

---

*If Microsoft can ship Windows 95 after Windows 3.11, we can ship v0.0.3 after v0.0.9.*

*That's not chaos. That's discipline.*

