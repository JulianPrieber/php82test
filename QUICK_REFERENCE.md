# Quick Reference: Best Laravel Link Shorteners (2025)

## TL;DR - Quick Answer

**Best Overall PHP Link Shortener:** [Shlink](https://github.com/shlinkio/shlink) (Symfony-based, not Laravel)
- ✅ Actively maintained (2024-2025)
- ✅ Modern, feature-rich, well-documented
- ✅ 3,000+ GitHub stars
- ✅ REST API, analytics, QR codes, multi-domain

**Best Laravel-Native Option:** Build custom or extend LinkStack
- LinkStack (current repo) already has most infrastructure needed
- Laravel-specific URL shorteners are outdated or unmaintained

## Active Projects Comparison

| Project | Tech Stack | Stars | Status | Last Update | License |
|---------|-----------|-------|--------|-------------|---------|
| **Shlink** | PHP/Symfony | 3,000+ | ✅ Active | 2024-2025 | MIT |
| **YOURLS** | PHP/Vanilla | 10,000+ | ✅ Active | 2024-2025 | MIT |
| **Polr** | Laravel | 4,900+ | ⚠️ Stale | 2020 | GPL-2.0 |
| **LinkStack** | Laravel | 2,000+ | ✅ Active | 2024-2025 | AGPL-3.0 |

## Why Shlink is Recommended

```bash
# Easy Docker deployment
docker run --name shlink -p 8080:8080 shlinkio/shlink:stable

# Or with docker-compose
version: '3'
services:
  shlink:
    image: shlinkio/shlink:stable
    ports:
      - "8080:8080"
    environment:
      - DEFAULT_DOMAIN=s.yourdomain.com
      - IS_HTTPS_ENABLED=true
```

### Key Features
- ✅ REST API for programmatic access
- ✅ Real-time visit stats & analytics
- ✅ QR code generation
- ✅ Custom short codes
- ✅ Multiple domains support
- ✅ Tags & organization
- ✅ PWA admin interface
- ✅ Import from other shorteners
- ✅ Regular security updates

## Alternative: Extend LinkStack

LinkStack already provides:
- User management
- Link analytics
- QR codes
- Custom domains
- Dashboard UI

**Add URL shortening in ~500 lines of code:**
- Database migration for short URLs
- ShortUrl model
- Controller for create/redirect
- Routes: `/s/{code}` for redirects
- Dashboard UI integration

See `URL_SHORTENER_IMPLEMENTATION.md` for full guide.

## Code Comparison

### Creating a Short URL in Shlink (API)
```bash
curl -X POST https://s.yourdomain.com/rest/v3/short-urls \
  -H "X-Api-Key: your-api-key" \
  -H "Content-Type: application/json" \
  -d '{"longUrl": "https://example.com/very-long-url"}'
```

### Creating a Short URL in LinkStack (proposed)
```php
$shortUrl = ShortUrl::create([
    'user_id' => auth()->id(),
    'short_code' => ShortUrl::generateUniqueCode(),
    'original_url' => 'https://example.com/very-long-url'
]);

echo $shortUrl->getShortUrl(); // https://yourdomain.com/s/abc123
```

## Decision Matrix

### Choose Shlink if you need:
- ✅ Battle-tested, production-ready solution
- ✅ Standalone URL shortening service
- ✅ Advanced analytics and reporting
- ✅ Multi-tenant domain management
- ✅ Enterprise features out of the box

### Choose to Extend LinkStack if you need:
- ✅ Unified platform (profiles + shortening)
- ✅ Tight Laravel integration
- ✅ Custom branding and theming
- ✅ Full control over source code
- ✅ Existing LinkStack infrastructure

### Avoid Polr because:
- ❌ Last update in 2020
- ❌ Security concerns with old dependencies
- ❌ No active maintenance
- ❌ Laravel version outdated

## Installation Time Comparison

| Solution | Setup Time | Complexity |
|----------|-----------|------------|
| Shlink (Docker) | 5 minutes | Low |
| YOURLS | 10 minutes | Low |
| LinkStack + Custom | 2-4 hours | Medium |
| Polr | Not Recommended | Medium |

## Resources

- **Shlink**: https://shlink.io
- **Shlink Docs**: https://shlink.io/documentation/
- **YOURLS**: https://yourls.org
- **LinkStack**: https://linkstack.org
- **Implementation Guide**: See `URL_SHORTENER_IMPLEMENTATION.md`
- **Full Research**: See `LARAVEL_LINK_SHORTENERS.md`

## Final Recommendation

**For immediate production use:** Deploy Shlink with Docker

```bash
# Quick start
git clone https://github.com/shlinkio/shlink-docker-compose
cd shlink-docker-compose
docker-compose up -d
```

**For LinkStack users:** Consider adding URL shortening feature to LinkStack for a unified experience

**For Laravel projects:** Build custom solution using Laravel's routing and ORM, inspired by Shlink's architecture

---

**Last Updated**: November 2025
**Document Purpose**: Quick reference for choosing URL shortener
**Next Steps**: See implementation guides in this repository
