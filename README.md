# Docker Compose Visualizer

A `docker-compose.yml` file is easy to write and hard to read back - `depends_on`
chains scroll off-screen, networks and volumes are declared far from where they're
used, and seeing what talks to what means scanning the whole file top to bottom.
Docker Compose Visualizer renders it as a live, editable diagram instead: service
cards wired by their real dependencies, updating as you type, editable by clicking
instead of hand-editing YAML.

![Two-way sync in action](docs/screenshots/demo-sync.gif)

`IntelliJ IDEA 2025.2+` · `Community & Ultimate` · `No Docker plugin required`

**Free to view, license required to edit** - the Architecture canvas and everything on
it is free, no strings attached. Clicking through to actually change something is the
paid part.

## Free to view

- **See the shape of your stack at a glance** - every service laid out by dependency
  order, not declaration order, with healthcheck, restart-policy, and mount status
  visible without opening the file.
- **Spot dead networks and volumes before they rot** - every network, volume, config,
  and secret in the file in one place, flagged if nothing actually uses it.
- **Catches problems before they bite you** - broken or circular service dependencies,
  two services publishing the same host port, and YAML that doesn't match the shape it
  expects are all flagged directly on the card, before you'd otherwise notice.
- **See what Docker actually runs** - the Effective Config view shows the merged result of
  your base file, override files, files under `include:` and selected profiles, resolved by the
  real `docker compose config` (Docker must be on your PATH). Each service and resource
  carries a chip naming the file that defines it. Works with a `COMPOSE_FILE` in `.env` too,
  so monorepos and non-standard file names are picked up.
- Also flagged: unrecognized `restart:` policies and `service_healthy` dependencies on a
  service with no healthcheck.
- Less common fields - long-form ports, per-network IP and alias settings, and more -
  are read and shown too, not just the common shorthand.

## Requires a license to edit

- **Edit services without fighting YAML syntax** - a focused form for the fields real
  compose services use most: image, environment, mounts, dependencies, networks.
- **Your comments and formatting survive every edit** - changes made in the diagram go
  straight back into your existing YAML file, not a regenerated copy of it.
- **Edit the merged result** - in Effective Config, a change is written to whichever file
  actually defines the value (base, override or included file), not just the one that's open.
- Add, attach, detach, and delete services, networks, volumes, configs, and secrets
  straight from the canvas.
- Scaffold a new Docker Compose file from the IDE's File > New menu.
- Anything the tailored form doesn't cover stays reachable through a built-in fallback
  editor, so nothing in your compose file is ever hidden.
- Confirms before deleting anything still in use, and shows how many services
  reference it. Blocks duplicate service names, invalid characters, and missing
  required fields before an edit can be saved.

## Screenshots

**Architecture canvas** - full view of a multi-service stack: cards in dependency
order, tags, and the resource summary underneath.

![Architecture canvas](docs/screenshots/screenshot-architecture.png)

**Service edit dialog** - the tabbed form open on a service, showing the Environment
or Mounts tab.

![Service edit dialog](docs/screenshots/screenshot-edit-dialog.png)

**Resource summary + warning** - the networks/volumes/configs/secrets row with an
unattached-resource warning visible.

![Resource summary](docs/screenshots/screenshot-resources.png)

## Requirements

- IntelliJ IDEA 2025.2 (build 252) or newer, Community or Ultimate. No Docker plugin
  required.

## Contributing

A sample compose file covering most supported fields is at
`samples/docker-compose.yml` - open it in the sandbox IDE from `./gradlew runIde` to
try things out. See `AGENTS.md` for contributor conventions and the project's
architecture.

## License

Use of the plugin is governed by its [End User License Agreement](https://github.com/devgrs1005/docker-compose-visualizer/wiki/EULA).
