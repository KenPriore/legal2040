# legal2040.kenpriore.ai — deploy

AUTHORING: the canonical page is Monito/money-matters-2040/money-matters.html (private repo).
This dir is the PUBLIC deploy copy. Never edit index.html here; re-copy from Monito after edits:
  cp ~/ClaudeCode/Monito/money-matters-2040/money-matters.html ~/ClaudeCode/legal2040-deploy/index.html
  cd ~/ClaudeCode/legal2040-deploy && git add -A && git commit -m "sync from Monito" && git push

FIRST DEPLOY (Ken runs):
  cd ~/ClaudeCode/legal2040-deploy
  gh repo create KenPriore/legal2040 --public --source=. --push
  gh api repos/KenPriore/legal2040/pages -X POST -f "source[branch]=main" -f "source[path]=/"
  # DNS (registrar): CNAME record  legal2040 -> kenpriore.github.io
  # If Pages shows a CNAME/domain error after DNS propagates: push an empty commit, never re-run setup.

VERIFY: by content hash, never by HTTP 200:
  curl -s https://legal2040.kenpriore.ai | md5
  md5 -q index.html
  (must match)

AT PUBLIC LAUNCH: delete the <meta name="robots" content="noindex"> line in the Monito canonical,
re-copy, push. The noindex is soft-launch only.

NOTE: the TLS cert appears in Certificate Transparency logs the moment Pages provisions it.
"Unlinked" is discoverable from that moment.
