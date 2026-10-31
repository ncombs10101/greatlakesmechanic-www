# greatlakesmechanic-www

Static site for **https://greatlakesmechanic.com** (Great Lakes ADAS Diagnostics, mobile mechanic service).
Plain HTML, no build step.

## Hosting

Served by **GitHub Pages** from the `main` branch (root), custom domain `greatlakesmechanic.com` (see `CNAME`).
Cloudflare DNS: `CNAME @ -> ncombs10101.github.io` and `CNAME www -> ncombs10101.github.io`, both DNS only.

Deploy = push to `main`. GitHub rebuilds in about a minute.

### Alternate: keystoneserver1

The same files can be served by Caddy on keystoneserver1 from a clone at `/tank/projects/greatlakesmechanic-www`:

```
greatlakesmechanic.com {
	root * /tank/projects/greatlakesmechanic-www
	encode zstd gzip
	file_server
	handle_errors {
		rewrite * /404.html
		file_server
	}
}

www.greatlakesmechanic.com {
	redir https://greatlakesmechanic.com{uri} permanent
}
```

To use it, point the A record at the server instead and turn GitHub Pages off.
