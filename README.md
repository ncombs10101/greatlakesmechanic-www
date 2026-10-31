# greatlakesmechanic-www

Static site for **https://greatlakesmechanic.com** (Great Lakes ADAS Diagnostics, mobile mechanic service).
Plain HTML, no build step.

## Hosting

Served from keystoneserver1 by Caddy. GitHub Pages is not used, so there is no `CNAME` file.

Document root: `/tank/projects/greatlakesmechanic-www` (a clone of this repo).

Caddy vhost:

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

## Deploying

```
git -C /tank/projects/greatlakesmechanic-www pull
```

No restart needed; Caddy serves from disk.
