# Local browser topology

This is the concrete browser AUTHOR setup on this Windows machine. Claude, Codex, or Hermes
may attach as the active EXECUTOR if the harness supports Chrome DevTools Protocol (CDP),
semantic element lookup, and bounded generation watching.

## Installed paths

- Chrome executable: `C:\Program Files\Google\Chrome\Application\chrome.exe`
- Persistent signed-in Chrome profile:
  `D:\Letters\MatTroiSeConMoc\Papers\User Generated\Hermes Chrome\profile`
- Chrome launcher:
  `D:\Letters\MatTroiSeConMoc\Papers\User Generated\Hermes Chrome\HERMES CHROME.vbs`
- Hermes configuration:
  `D:\Letters\MatTroiSeConMoc\Products\Hermes\State\config.yaml`

The account selected by the creator is already signed in inside that persistent profile. Do
not record its email, cookies, tokens, or credentials here.

## Endpoints

- CDP root: `http://127.0.0.1:9222`
- Browser health/version: `http://127.0.0.1:9222/json/version`
- Open targets: `http://127.0.0.1:9222/json/list`
- Expected AUTHOR origin: `https://chatgpt.com/`

The launcher starts Chrome with:

```text
--remote-debugging-address=127.0.0.1
--remote-debugging-port=9222
--user-data-dir="D:\Letters\MatTroiSeConMoc\Papers\User Generated\Hermes Chrome\profile"
--no-first-run
--no-default-browser-check
```

Hermes uses:

```yaml
browser:
  cdp_url: http://127.0.0.1:9222
```

Start a fresh Hermes session after changing browser configuration.

## Attaching another harness

1. Run `HERMES CHROME.vbs` if the endpoint is not already healthy.
2. Read `/json/version`; do not proceed unless the endpoint answers on loopback.
3. Read `/json/list` and find the ChatGPT page by origin plus its expected current title.
   Titles change, so a title alone is not identity.
4. Retain the returned opaque target ID and revalidate that it still maps to ChatGPT before
   every mutation.
5. Drive the claimed tab by accessibility role or semantic DOM identity, never guessed screen
   coordinates.
6. Only one EXECUTOR may own and mutate the claimed AUTHOR tab at a time. Never touch
   unrelated tabs.
7. Verify prompt submission, observe generation start, and wait for generation to finish
   before reading the final response.

Attach to the existing endpoint when continuing the shared AUTHOR conversation. For
independent concurrent browser work, launch a different durable profile on a different
loopback port. Never start a second Chrome process against the profile above, copy it while
Chrome is running, reuse port `9222`, or expose CDP to the LAN.
